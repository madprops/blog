# History

Today I decided to improve the history in fish shell.

This is what needed to be done:

1) The commands will be saved with the unix timestamp and the current working directory.
This is to use with grep-like commands later, since the context is useful.

1) A new function is to be made to display the contents of this file with an optional grep argument. It wil use the timestamps to show relative times like "2 months ago". Because I personally avoid any visible exact date string due to privacy reasons, and the relative format is easier to understand anyway. The newer items appear at the bottom, to avoid having to scroll or using `head`.

1) All terminals will read and write using this file, it's not like the default behavior of using history data per session, that's very annoying.

1) The up/down arrow functionality will now use this new history file.

---

Add this to your fish config file:

```fish
function log_command --on-event fish_preexec
  set -l command (string join " " -- $argv)
  set -l first_word (string split -n -m 1 " " -- $command)[1]
  if contains -- $first_word fh ls cd
      return
  end

  set -l cwd (pwd)
  set -l log_dir ~/.config/fish

  if not test -d "$log_dir"
      mkdir -p "$log_dir"
  end

  echo (date +%s)"|$command|$cwd" >> "$log_dir/fishy_history.txt"

  # Reset history cache
  set -e _fishy_history_cache
  set -e _fishy_history_index
end

function fh
  set -l history_file ~/.config/fish/fishy_history.txt
  set -l filter (string join " " -- $argv)

  if not test -f $history_file
    echo "History file not found: $history_file"
    return 1
  end

  if test -n "$filter"
    grep -i -- "$filter" $history_file
  else
    tail -n 1000 $history_file
  end | python -c '
import sys, time, re
now = time.time()

def parse_line(line):
    line = line.strip()
    if not line: return None
    try:
        if "|" in line and line.count("|") >= 2:
            rest, cwd = line.rsplit("|", 1)
            ts_str, cmd = rest.split("|", 1)
        else:
            m = re.match(r"^(\d+)\s+(.*?)>(.*)$", line)
            if not m: return None
            ts_str, cwd, cmd = m.groups()
            cwd, cmd = cwd.strip(), cmd.strip()
        return float(ts_str), cmd, cwd
    except: return None

lines = sys.stdin.readlines()
parsed = []
for line in lines:
    p = parse_line(line)
    if p: parsed.append(p)

# Deduplicate keeping latest
seen = set()
unique = []
for item in reversed(parsed):
    cmd = item[1]
    if cmd not in seen:
        seen.add(cmd)
        unique.append(item)

# Take last 20 (which are first 20 in reversed list)
unique = unique[:20]
# Reverse back to chronological order
unique.reverse()

for ts, cmd, cwd in unique:
    diff = now - ts
    if diff < 0: diff = 0

    if diff < 60: ago = f"{int(diff)}s ago"
    elif diff < 3600: ago = f"{int(diff/60)}m ago"
    elif diff < 86400: ago = f"{int(diff/3600)}h ago"
    else: ago = f"{int(diff/86400)}d ago"

    print(f"({ago}) {cmd} \033[90m({cwd})\033[0m")
'
end

function fishy_up
  if not set -q _fishy_history_cache
    set -l history_file ~/.config/fish/fishy_history.txt
    if test -f $history_file
      set -g _fishy_history_cache (tail -n 1000 $history_file | python -c '
import sys
lines = sys.stdin.readlines()
seen = set()
for line in reversed(lines):
    line = line.strip()
    cmd = ""
    if "|" in line and line.count("|") >= 2:
        try:
            rest, _ = line.rsplit("|", 1)
            _, cmd = rest.split("|", 1)
        except: continue
    elif ">" in line:
        cmd = line.split(">", 1)[1].strip()

    if cmd and cmd not in seen:
        seen.add(cmd)
        print(cmd)
')
    end
    set -g _fishy_history_index 0
  end

  set -l count (count $_fishy_history_cache)
  if test $count -eq 0
    return
  end

  set -g _fishy_history_index (math $_fishy_history_index + 1)

  if test $_fishy_history_index -gt $count
    set -g _fishy_history_index $count
  end

  commandline -r -- $_fishy_history_cache[$_fishy_history_index]
end

function fishy_down
  if not set -q _fishy_history_index
    return
  end

  set -g _fishy_history_index (math $_fishy_history_index - 1)

  if test $_fishy_history_index -le 0
    set -g _fishy_history_index 0
    commandline -r ""
  else
    commandline -r -- $_fishy_history_cache[$_fishy_history_index]
  end
end

bind \e\[A fishy_up
bind \e\[B fishy_down
bind up fishy_up
bind down fishy_down
```

---

As an additional note, I tried the new Gemini 3 to work on this and it worked wonderfully. It did things correctly where other models failed. Interestingly it was the only model that considered using python strings for advanced operations.
# Commands

I was missing a way to re-run commands quickly from my terminals.

I use up-arrow-rewind or autocomplete to run previous commands.

But that can get annoying sometimes, I wanted something to click.

So here it is:

## Fish

Add this to `~/.config/fish/config.fish`:

```bash
function intercept --on-event fish_postexec
  if [ "$status" != 0 ]
    return
  end

  ~/bin/save_command $argv
end
```

This will run a ruby script after every succesful command.

## Ruby

This is the script that gets called to update the commands file:

>save_command

```ruby
#!/usr/bin/env ruby
cmd = ARGV[0].strip
xcmds_equals = ["cd", "ls", "lq", "z", "br", "o"]
xcmds_starts = ["cd", "z"]

if xcmds_equals.any? { |x| cmd == x }
  return
end

if xcmds_starts.any? { |x| cmd.start_with?(x) }
  return
end

xhistory = File.expand_path("~/.xhistory.log")
max_xhistory = 500
lines = []

File.open(xhistory, "a+") do |file|
  lines = file.readlines
end

lines.prepend(cmd)
content = lines.map(&:chomp).uniq.take(max_xhistory).join("\n")

File.open(xhistory, "w") do |file|
  file.puts(content)
end
```

This is the script that opens `rofi` to pick a command:

>commands

```ruby
#!/usr/bin/env ruby
require "open3"

def pick_cmd(prompt, data)
  cmd = "rofi -dmenu -p '#{prompt}' -me-select-entry '' -me-accept-entry 'MousePrimary' -i"
  stdin, stdout, stderr, wait_thr = Open3.popen3(cmd)
  stdin.puts(data.split("\n"))
  stdin.close
  return stdout.read.strip
end

fname = File.expand_path("~/.xhistory.log")
data = File.read(fname).strip
cmd = pick_cmd("Select Command", data)

if cmd.empty?
  return
end

system("xdotool type '#{cmd}'")
system("xdotool key Return")
```

## awesomewm

Now in `awesomewm` do something similar to this:

```lua
function commands()
  local c = mouse.object_under_pointer()

  if not c then
    return
  end

  local cmds = {"dolphin", "tilix"}

  if table_contains(cmds, c.instance) then
    focus(c)
    show_commands()
    return
  end
end

function focus(c)
  c:emit_signal("request::activate", "tasklist", {raise = true})
end

function home_bin(cmd)
  awful.spawn(os.getenv("HOME") .. "/bin/" .. cmd)
end

function show_commands()
  home_bin("commands")
end

table_contains(tab, val)
  for index, value in ipairs(tab) do
    if value == val then
      return true
    end
  end

  return false
end
```

Run this function on a mouse or keyboard press.

This will first focus the client, then run the ruby script called `commands`.

## Usage

Now when you press a specific button on a specific window, it will show `rofi` with the latest commands.

You can click or press enter and `xdotool` will write the command on the focused window.

It will automatically press Enter. You might want to disable that by commenting the last line.

Since it's `rofi` you can also filter it through the keyboard.

It's meant to target terminal emulators.

I suggest saving it as `~/bin/commands`.

Also I suggest adding `~/bin` to the path.

![](https://i.imgur.com/ajk8iWQ.jpg)
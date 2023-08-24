# Commands

I was missing a way to re-run commands quickly from my terminals.

I use up-arrow-rewind or autocomplete to run previous commands.

But that can get annoying sometimes, I wanted something to click.

So here it is:

## Fish

First create this file:

`touch ~/.local/share/fish/xhistory.log`

This is where (some) of the command history will be stored.

Some common irrelevant commands like `ls` and `cd` get ignored.

Then add this to `~/.config/fish/config.fish`:

```bash
set xhistory ~/.local/share/fish/xhistory.log
set max_xhistory 500

function intercept --on-event fish_postexec
  if [ "$status" != 0 ]
    return
  end

  set cmd (string trim $argv)

  if string match -q "cd" $cmd
    return
  end

  if string match -q "cd *" $cmd
    return
  end

  if string match -q "ls" $cmd
    return
  end

  echo "$cmd\n" >> $xhistory
  awk '!seen[$0]++' $xhistory >$xhistory_tmp && mv $xhistory_tmp $xhistory
  set log_size (count (cat $xhistory))

  while test $log_size -gt $max_xhistory
    sed -i 1d $xhistory
    set log_size (count (cat $xhistory))
  end
end
```

This will run a function after every command.

If the last command failed it will return early.

It filters out some common short commands.

Then it saves to the file, removes duplicates, and applies the `max_xhistory` limit.

Everytime you modify `config.fish` you need to source it again:

`source ~/.config/fish/config.fish`

I recommend this alias:

`alias sauce="source ~/.config/fish/config.fish"`

## awesomewm

Now in `awesomewm` do something similar to this:

```lua
function commands()
  local c = mouse.object_under_pointer()

  if not c then
    return
  end

  if c.instance == "dolphin" then
    focus(c)
    show_commands()
    return
  end

  if c.instance == "tilix" then
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
```

Run this function on a mouse or keyboard press.

This will first focus the client, then run the ruby script called `commands`.

## Ruby

```ruby
#!/usr/bin/env ruby
require "open3"

def pick_cmd(prompt, data)
  cmd = "rofi -dmenu -p '#{prompt}' -me-select-entry '' -me-accept-entry 'MousePrimary' -i"
  stdin, stdout, stderr, wait_thr = Open3.popen3(cmd)
  stdin.puts(data.split("\n").reverse)
  stdin.close
  return stdout.read.strip
end

fname = File.expand_path("~/.local/share/fish/xhistory.log")
data = File.read(fname).strip
cmd = pick_cmd("Select Command", data)
system("xdotool type '#{cmd}'")
system("xdotool key Return")
```

## Usage

Now when you press a specific button on a specific window, it will show `rofi` with the latest commands.

You can click or press enter and `xdotool` will write the command on the focused window.

It will automatically press Enter. You might want to disable that by commenting the last line.

Since it's `rofi` you can also filter it through the keyboard.

It's meant to target terminal emulators.

I suggest saving it as `~/bin/commands`.

Also I suggest adding `~/bin` to the path.

![](https://i.imgur.com/ajk8iWQ.jpg)

## Notes

Possible expansion is to limit commands by being aware of the directory...

So each directory gets the most relevant commands to them.

You'd need to save lines in the file differently like `dir ; cmd`.

But right now I don't want to do that.
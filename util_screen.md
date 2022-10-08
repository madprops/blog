# Util Screen

I used to have my file manager in a fixed virtual desktop, visible at all times.

I decided to replace that with a browser instance to have a mini video player.

But where should I put the file manager now?

I thought, what if I could pull it down like I do with my terminal?

With my terminal I press a button on my keyboard to toggle its visiblity.

I asked around and found some actual solutions to this dropdown functionality.

For instance [this](https://blingcorp.github.io/bling/#/module/scratch)
 , [and this](https://github.com/lcpz/lain/wiki/Utilities#quake)
 , [and this](https://docs.qtile.org/en/stable/manual/config/groups.html?highlight=scratchpad#scratchpad-and-dropdown).

I decided to use none of those. First because my window manager setup has no 3rd party dependencies yet, and I wanted to keep it that way.

Also because I had the idea that instead of having a dropdown terminal and a dropdown file manager, I could have a layout with both of them.

So I created a layout with some window rules for the file manager, the terminal, and a calculator (SpeedCrunch) because why not.

I gave the util applications a special `xutil` property to treat them as such.

Now I only need to bring those windows to the current virtual desktop and hide them when I don't need them anymore.

```lua
-- Used once to start the applications
function Utils.start_util_screen()
  Utils.spawn("dolphin")
  Utils.spawn("speedcrunch")
  Utils.spawn("tilix --session ~/other/tilix.json")
end

-- When I press the key do this
function Utils.toggle_util_screen()
  if Utils.util_screen_on then
    local highest = Utils.highest_in_tag(Utils.util_screen_tag)

    if not Utils.util_screen_tag.selected or (highest ~= nil and not highest.xutil) then
      Utils.show_util_screen()
    else
      Utils.hide_util_screen()
    end
  else
    Utils.show_util_screen()
  end
end

-- Show the util applications
function Utils.show_util_screen()  
  local t = Utils.mytag()
  
  for _, c in ipairs(client.get()) do
    if c.xutil then
      c:move_to_tag(t)
      c:raise()
      Rules.reset_rules(c)
      c.hidden = false
    end
  end
  
  Utils.util_screen_on = true
  Utils.util_screen_screen = Utils.myscreen()
  Utils.util_screen_tag = Utils.mytag()
end

-- Make them invisible
function Utils.hide_util_screen()
  for _, c in ipairs(client.get()) do
    if c.xutil then
      c.hidden = true
    end
  end

  Utils.util_screen_on = false
end
```

It does several checks to know if the util screen should be shown or not, to make it feel as natural as possible.

## So how do I use it?

When I need to use files, or the terminal, or the calculator, I spawn the util screen on the opposite monitor that I'm using.

Or on the same monitor if if that makes more sense.

That's the point of having a dropdown util screen, it's flexible enough to land anywhere I need it.

And when I don't need the util screen anymore I just hide it.

![](https://i.imgur.com/mbYwsps.jpg)

Maybe I should think of a cooler name other than "util screen" though.
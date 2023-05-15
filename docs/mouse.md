# Mouse

![](https://i.imgur.com/h6aEPZp.jpg)

I use the Roccat Kova for various reasons:

1) There's a program for linux to customize it.
Although it won't work with the new Kova.
I had to recompile it with some modifications.

2) It has TopSide buttons (left and right). These are two extra buttons at my fingertips close to the main buttons. Easy to use.

3) The DPI button can be mapped to something and it's easy to use.

4) It's ambidextrous.

## How do I use it

First of all, I use the mouse a lot, I don't believe in the keyboard-driven mentality that tries to undermine the mouse. Although I do use the keyboard heavily, not just for typing but for shortcuts.

I program the buttons by mapping them to keyboard shortcuts, and then mapping those shortcuts to actions in my window manager.

The TopSide buttons are used to quickly switch between desktops. For instance if I press the TopRight I can go from Desktop 1 to Desktop 2. By that I mean linux virtual desktops.

The DPI button is mapped to a piece of code that detects the window under the cursor and closes it. But if it's a browser instance it then closes the tab using Ctrl+W instead. This only works if the button is pressed twice in quick succesion to avoid accidents. This is all handled by my window manager using lua (awesomewm).

The SideForwards button is dedicated to playing and stopping music. Sometimes I map it directly to playerctl play-pause, but lately it triggers some little rofi-based player manager I made.

The SideBackwards button is simply mapped to the Esc key.
This turned out to be a great idea, it's incredibly useful. Why? Because if you think about it, Esc is used everywhere, all the time throughout many types of applications. I can just keep my hand on the mouse and dismiss stuff instead of reaching out to my keyboard.

## Gestures

Gestures are a nice way to control more things by moving the mouse in certain shapes. I've used various tools to achieve this on linux. There's a program called EasyStroke that was dedicated to doing this but I think it was abandoned. KDE has its own gestures manager which works nicely. What I currently use is the Gesturefy extension for Firefox to Go-To-Top, Go-To-Bottom, Go-Back, Go-Forward, Refresh. This allows me to navigate the web faster.

## Util Screen

There's a [blog post](https://github.com/madprops/blog/blob/main/util_screen.md) I made about the util screen which drops down a bunch of utils in whatever monitor I choose. To trigger this I programmed my window manager to detect clicks of the DPI button at the top of the screen:

```lua
awful.key({modkey}, "Delete", function()
  if mouse.coords().y <= 25 then
    Utils.toggle_util_screen()
    return
  end

  closetap.trigger()
end)
```

So I can spawn and dismiss the utils with my mouse very easily.

## Move To Desktop

A small thing I added is the ability to right click the number of a desktop and send the active window to that desktop.

![](https://i.imgur.com/OwPtFde.jpg)

For instance if I have the window in desktop 2 and I simply right click '4', the window is sent to desktop 4 (and the desktop gets focused).

## Menupanel

I developed a menu system within my window manager which I use for several things, including a context menu when right-clicking taskbar items.

![](https://i.imgur.com/1LBENZT.jpg)
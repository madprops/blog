# Timers

Lately I've been using timers daily.

By that I mean timeouts, for example 20 minutes:

- Start at 20 minutes

- Slowly goes down to 0

But it mostly makes sense if I add a visual widget for it.

So I built one baked into my wm:

![](https://i.imgur.com/hRmYjp3.jpg)

This appears in the panel once I start a timer.

It will update every second.

Eventually it goes into seconds:

![](https://i.imgur.com/W49rAeT.jpg)

Then it reaches 0 and disappears.


## Actions

I can map a function as an action for when the timer is done.

It can be a simple "Timer Ended" message, or an action like "suspend the computer".

Now I don't suspend the computer immediately, I activate a 60 or 90 minute timer.

Which gives me time to go back and check something without having to turn the computer on.

![](https://i.imgur.com/7QuoafS.jpg)

## Time to Think

I've been using timers before releasing new versions of software.

Before, I would publish pretty much immediately thinking there's nothing more to do.

But now I start a timer depending on how confident I am about the changes.

The bigger the change the higher the timer.

And I won't consider releasing the version until the timer ends.

This gives me time to test the application and find flaws or missing things.

And it actually happens very often, that I find things to add or polish.

## Mouse Wheel

An interesting feature I added  to the timer widget, that I actually use a lot.

I can use the mousewheel when hovering the widget to increase or decrease the timer.

It increases or decreases by 5 minutes.

And it will round to the nearest 5 minute step.

For instance 3 minutes -> 5 minutes -> 10 minutes -> 15 minutes.

It allows me to adjust how much I'm willing to wait for something.

Depends on my judgment if a timer should increase or decrease.

The minimum is 1 minute, it won't go below it with the mousewheel.

![](https://i.imgur.com/dJHwGBY.gif)

## Middle Click

Middle clicking the widget cancels the timer.

## Multiple Timers

Any number of timers can be started.

As long as they have a different name:

![](https://i.imgur.com/f9O9mrk.jpg)

## Counters

The timer widget/library also supports "counters".

These are the opposite. They start at 0 and go upwards.

![](https://i.imgur.com/pFOu0jF.jpg)

## Code

Some code of how I start the timers with my wm:

![](https://i.imgur.com/I2lzmBK.jpg)

## Other Uses

It's also useful for measuring non-computer activities.

Like waiting for food or drinks to be ready.

## Starting Timers

Since my wm can be called through a special program, I can make a python script to start timers.

I made a script that makes it easy to detect if I want hours, minutes, or seconds.

So I can easily start a 20 minute timer, or a 5 second timer. 

And I can do it directly from my launcher.

![](https://i.imgur.com/wPtPpH3.jpg)

## Repo

The code for autotimer is [here](https://github.com/madprops/awesome-setup/tree/master/madwidgets/autotimer).
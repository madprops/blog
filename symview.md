# Symview

![](https://i.imgur.com/K7Lik8x.gif)

This is how I often find images in my images collection.

I use this when I want to find an image by its file name.

I have images scattered in multiple directories.

Symview matches the file name but does one more thing...

## /tmp/ Symlinks

I want to see the image results with their thumbnails.

Would be nice to open a file manager window with these.

/tmp is a special places in linux that is not permanently stored.

AFAIK it gets resetted on each reboot.

So I decided to create symlinks of the results in `/tmp/symview_results`.

And I open this with Konqueror (my main file manager is Dolphin).

## How does it work?

I use a python program I made called Symview.

Symview can be told to find images, audio, video, or all.

`python /path/to/symview.py images dinosaur`

I use Rofi to get user input.

1) Find recursively all images in a path that match some string.

2) Clear `/tmp/symview_results`.

3) Create a symlink of each image in `/tmp/symview_results`.

4) Open a file manager instance on `/tmp/symview_results`.

## What Do You Get?

You get a window full of symlinks (these are cheap).

Which means you have references to the original files.

You can easily open them in an image viewer.

You can drag them to upload forms.

Or whatever.

## Why Not Just Search With Dolphin?

I found its search to be unreliable sometimes.

Especially since I don't use KDE with baloo.

Also dedicating Konqueror for this use-case is nice.

Symview is fast, and works fine for me.

---

You can see the code [here](https://github.com/madprops/symview).
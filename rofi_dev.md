# Developing Tools With Rofi

[Rofi](https://github.com/davatorium/rofi) is a linux program.

It allows me to do several things:

- Launch applications
- Switch to open windows
- Show information
- Filter information
- Ask for information

Here's how launching applications can look like:
![](https://i.imgur.com/9rcbhil.jpg)

Filtering is built-in and usable in different modes.

## Using Information

To generate the items you pass linebreak-separated lines:

```python
proc = Popen(f"rofi -dmenu -i -p '{path}'", stdout=PIPE, stdin=PIPE, shell=True, text=True)
ans = proc.communicate("\n".join(items))[0].strip()
```

## Getting Information

Rofi can return information after it finishes running.

It can return either of these:

- The index of the item you picked
- The text of the item you picked
- The text you wrote before pressing Enter

This is useful when you need to prompt for arguments.

Here I have a program that searches for images.

If you run the program without arguments, it can use rofi to get the input:

![](https://i.imgur.com/GKNQah3.gif)

This is the function I used in the above example:

```python
# Get input information using rofi
def get_input(prompt: str) -> str:
  proc = Popen(f"rofi -dmenu -p '{prompt}'", stdout=PIPE, stdin=PIPE, shell=True, text=True)
  return proc.communicate()[0].strip()
```  

## Desktop Files

Adding entries to the application launcher is easy.

(This is true for any launcher in linux)

All you do is go to ~/.local/share/applications

And make a file called something.desktop

Which can look like this:

```
[Desktop Entry]
Version=1.0
Name=counter
Comment=Count Stuff
GenericName=counter
Exec=/home/user/scripts/counter.sh
Icon=application-x-executable
StartupNotify=true
Terminal=false
Type=Application
```

Now it's visible to rofi in launch mode.

I recommend using a prefix for your .desktop files.

Something like `w_counter.desktop`

So you know `w_` files are your custom ones.

## Clipton

I made a clipboard manager using python and rofi.

It saves clipboard data in a json file.

Feeds the lines of text to rofi via a subprocess.

Allows the user to select an item (filtering works).

It receives the index and puts the item in the clipboard.

It also supports some Alt+Number commands.

I added some features like joining several items into a single line on demand.

And fetching URL titles automatically as seen in the screenshot.

![](https://i.imgur.com/20ef1JU.jpg)

[Clipton Repo](https://github.com/madprops/clipton)

## Empris

playerctl manager using python and rofi

Able to show, play, stop, media players:

![](https://i.imgur.com/nCKRdWe.jpg)

[Empris Repo](https://github.com/madprops/empris)

## Ezkl

For a directory bookmark/jumper I made I use rofi when there's ambiguity.

As you can see, the first two commands go straight to the directories.

But the third one has 2 possible results, so rofi asks for clarification:

![](https://i.imgur.com/hIIzaIW.gif)

[Ezkl Repo](https://github.com/madprops/ezkl)

## OpenFile

I'm also working on a rofi-based tool to navigate the file system.

It shows [+] for directories. It can go back. It can create new files.

It's also compatible with ezkl for directory jumping.

Upon exit it returns a path, which you can use to open in programs.

![](https://i.imgur.com/kK2dWjM.gif)

[OpenFile Repo](https://github.com/madprops/openfile)

## Styling

Rofi can be themed.

It can also be customized per instance using css-like rules.

`-theme-str "window {height: 200px;}"`
# JStyle

These are some of my current javascript standards.

You'll likely disagree with them but that's expected and don't want to hear it.

## Main Object

Everything resides inside an object called App.

```js
const App = {}
```

Every global variable and function go in there.

```js
App.last_date = Date.now()

App.say_hi = () => {
  //
}
```

This acts in a way as a global namespace, but it's a namespace you fully control.

```js
App.say_hi()
```

You can use strings to get variables or functions:

```js
App[`print_${what}`]()
```

You can do this with global namespaces like `window` but that can get messy.


## Imports

Imports go inside App.i

```js
App.i = {}
App.i.fs = require(`fs`)
App.i.path = require(`path`)
```

Now you always now if you're dealing with an import.

## Backticks

All strings are made with backticks.

```js
let name = `Elvis Presley`
let place = `Cape ${thing}`
```

This way you don't mix string formats and you always can insert variables easily.

This also allows free usage of single quotes and double quotes inside the string.

The only exception is when you need to fill some object with a multi-word string:

```js
{
  "Some Thing": 123
}
```

Since backticks are not permitted there for some reason.

## Arrow Functions

Arrow functions are used always.

```js
App.shout = (x) => {
  // Something
}
```

Simply because it's shorter and makes code neater.

Just be careful when you try to use `this`.

Functions with a single parameter still use parenthesis `(x) =>`.

Except on functional programming operations like `.filter(x => x > 1)`.

## Semicolons

Semicolons at the end of lines are never used. They are unnecessary and make the code ugly.

## If Else | Try Catch | Then Catch

Each component is joined, touching, after a linebreak:

```js
if (a) {
  //
}
else if (b) {
  //
}
else {
  //
}

try {
  //
}
catch (err) {
  //
}

do_something()
.then(x => {
  //
})
.catch (err => {
  //
})
```

## Underscores

Underscores are used to separate name components like variables.

```js
App.last_game_of_summer = 123
```

It's easy to read and is never ambiguous like it can happen with camelCase.

## Filling The App Object

As you create more js files as modules, you send them the App object and it gets filled.

In the case of node:

```js
module.exports = (App) => {
  App.something = () => {
    //
  }

  // More functions
}
```

And you fill it like:

```js
require(`./my_module`)(App)
```

In the case of frontend the App object is already global:

```js
App.something = () => {
  //
}

// More functions
```

## Trailing Commas

Lists always have a trailing comma:

```js
let list = [
  `item_1`,
  `item_2`,
]
```

This makes it easier to work with since you can freely move items around.

## Spacing

Use space between outer tokens and parenthesis:

```js
if (something) {
  //
}
```

## Brackets

Brackets start on same line, ends on newline:

```js
App.play = () => {
  //
}

if (a) {
  //
}
```

## Default Parameters

Default parameters use some spacing between the `=`.

```js
App.greet = (a, b = `Tom`) => {
  //
}
```

## Many Arguments

When functions use more than 3 arguments, an `args` object is preferred.

```js
App.machine_play = (args) => {
  if (args.name === `Media Luna`) {
    //
  }

  if (args.save) {
    //
  }
}
```

```js
App.machine_play({
  name: `Pepe`,
  save: true,
  age: 1234,
  team: `AMD`,
  strip: false,
  play: true,
})
```

If you want to use defaults you can use `def_args` like this:

```js
App.machine_play = (args) => {
  let def_args = {
    edited: false,
    save: true,
  }

  args = Object.assign(def_args, args)
}
```

This way, the args objects can have as many arguments as you want.

While not complicating function calls too much.

## For Loops

When using classic `for` loops, this is the spacing I use:

```js
for (let i=0; i<stuff.length-1; i++) {
  //
}
```

Instead of using a lot of spacing, each component is a bit tighter.

This makes it easier to read.

Avoid `forEach`. Use `for of` as much as you can.

The latter is more natural and allows normal usage of `continue`, `break`, and `return`.

```js
for (let item of items) {
  //
}
```

## General Spacing

This part is mostly personal instinct.

I like to join as much as I can in chunks.

And separate lines from multi-line or other statements.

Whatever feels right really.

```js
let a = 1
let b = 2

if (a) {
  //
}

do_that()
do_this()

let c = 3
```

## Object Spacing

Space between `:` and the value:

```js
{a: 123, b: 456}
```

## Long Objects

When objects get too long, use a multi-line format:

```js
let cat = {
  name: `Chains`,
  size: 123,
  catnip: true,
  // etc
}
```

## Parenthesis And Bracket

Usually the parenthesis can go alongside the bracket:

```js
do_this({
  //
})

do_this(`Balls`, {
  //
})

do_this(`Balls`, {
  //
}, 123)
```

This depends on what you're doing and what feels right.

## Comments

Only write comments when something is not obvious.

Or if it can take a while to understand what it is doing.

Usually what a function does can be deduced by its name.

## Init

(Client) The main function is called on window load in the main html file:

```js
window.onload = () => {
  App.init()
}
```

You start everything there.

## DOM Functions

I wrote helper functions to deal with the DOM:

```js
// Select a single element
App.el = (query, root = document) => {
  return root.querySelector(query)
}

let c = App.el(`#container`)

// Select an array of elements
App.els = (query, root = document) => {
  return Array.from(root.querySelectorAll(query))
}

let items = App.els(`.items`)

// Add an event listener
App.ev = (element, action, callback, extra) => {
  element.addEventListener(action, callback, extra)
}

App.ev(App.el(`#canvas`), `click`, () => {
  //
})
```

These might be inside an `utils` or `dom` object.

## Input

I usually add mouse events on specialized setup functions:

```js
App.setup_buttons = () => {
  App.ev(App.el(`#button`), `click`, () => {
    App.do_something()
  })

  // Etc
}
```

Or bind them when building elements dynamically at runtime.

I use a single global keyboard function for all key detection:

```js
App.setup_keyboard = () => {
  App.ev(document, `keydown`, (e) => {
    if (e.key === `Enter`) {
      App.do_something()
      e.preventDefault()
    }

    // Etc
  })
}
```

## Frameworks

I don't use frontend frameworks like `React` or `Vue`.

I assemble all connections manually.

So far it has worked for me, even on complex applications.

I do use specialized helper libraries when needed.

## Templates

I use `ejs` templates heavily through [Handlebars](https://handlebarsjs.com/).

They're special files or snippets you can use to generate `html`.

A template can look like this:

```html
<script id="template_whispers" type="text/x-handlebars-template" class="template">
  {{{window_controls}}}
  <div id="whispers_container" class="something"></div>
</script>
```

I have a function that compiles all templates:

```js
// Create all the Handlebars templates
App.setup_templates = () => {
  for (let template of App.els(`.template`)) {
    App[template.id] = Handlebars.compile(App.el(`#${template.id}`).innerHTML)
  }
}
```

That creates a bunch of functions like `App.template_whispers`.

I can use it like this:

```js
let html = App.template_whispers({
  window_controls: App.template_window_controls({
    filter_mode: `auto`,
  })
})
```

Then set some element to use that html.

## Windows

I wrote a windowing system which I use on my applications, called [Msg](https://merkoba.github.io/Msg/).

It handles modals, popups, and other form of windows.

It helps me control the window state since it knows what is open or not.

It allows me to open and close windows through its functions.

It handles multi-layered modals and stacked popups.

I create windows like this:

```js
let msgvars = {}

msgvars.common = {
  show_effect: `none`,
  close_effect: `none`,
  // Etc
}

msgvars.titlebar = {
  enable_titlebar: true,
  center_titlebar: true,
  // Etc
}

// Create all windows

App.msg_profilepic = Msg.factory(
  Object.assign({}, msgvars.common, msgvars.titlebar, {
    id: `profilepic`,
  })
)

App.msg_profilepic.set(App.template_profilepic())
App.msg_profilepic.set_title(`Some Title`)
```

Then I can control the window:

```js
App.msg_profilepic.show(() => {
  // Window is now open
  // Do something
})

App.msg_profilepic.close()
```

## Building Elements

Something I do very often is build and insert DOM elements on the fly.

I made a helper function for this:

```js
// Create an html element
App.create = (type, classes = ``, id = ``) => {
  let el = document.createElement(type)

  if (classes) {
    let classlist = classes.split(` `).filter(x => x != ``)

    for (let cls of classlist) {
      el.classList.add(cls)
    }
  }

  if (id) {
    el.id = id
  }

  return el
}
```

A simple example can be:

```js
let container = App.create(`div`, `action bright`, `main_container`)
```

There I created a div with classes `.action` and `.bright`, and with id `#main_container`.

You can add stuff to it:

```js
let item = App.create(`div`)

App.ev(item, `click`, () => {
  //
})

container.append(item)
```

There I created an item, added a mouse event, and attached it to the container.

```js
App.el(`#main`).append(container)
```

There I added the container to a main DOM element.

## console.log

If you're going to print messages as part of the system, use `console.info`.

If you're going to print errors use `console.error`.

Use `console.log` only for debugging. And make sure to remove them before pushing the code.

Best is to have a custom centralized function for logging:

```js
App.log = (message, mode = `normal`) => {
  if (mode === `error`) {
    console.error(message)
  }
  else {
    console.info(`🟢 ${message}`)
  }
}
```

## NeedContext

Apart from Msg, I made a simple library to handle context menus.

This can be triggered on right click or simple clicks on elements.

The library is called [NeedContext](https://github.com/madprops/needcontext).

Menus are built like this:

```js
App.show_some_context = (x, y) => {
  let items = []

  items.push({
    text: `Copy URL`,
    action: () => {
      App.copy_url()
    }
  })

  items.push({
    text: `Copy Title`,
    action: () => {
      App.copy_title()
    }
  })

  NeedContext.show(x, y, items)

  // Or

  NeedContext.show_on_element(el, items)
}
```
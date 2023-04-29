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

All strings are backticks.

```js
let name = `Elvis Presley`
let place = `Cape ${thing}`
```

This way you don't mix string formats and you always can insert variables easily.

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

Brackets start on same line, ends in newline:

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
    save: true
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
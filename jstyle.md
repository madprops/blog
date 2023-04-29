# JStyle

These are some of my current javascript standards.

You'll likely disagree with them but that's expected and don't want to hear it.

## Main Object

Everything resides inside an object called App.

```js
const App = {}
```

Every variable and function go in there.

```js
App.last_date = Date.now()

App.say_hi = () => {
  console.log("hi")
}
```

This acts in a way as a global namespace, but it's a namespace you fully control.

```js
App.say_hi()
```

You can use variables to call functions:

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

No exception. This way you don't mix string formats and you always can insert variables easily.

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

Semicolons at the end of lines are never used. They are unecessary and make the code ugly.

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

It's simply easy to read and is never ambiguous like it can happen with camelCase.

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
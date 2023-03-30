# airc (ai + irc)

Around 2 weeks ago I decided to finally give in to the novelty of chatGPT.

I decided to make an irc bot that would make requests to the openai api.

I thought it could become some sort of consultant people in my irc room can ask questions to.

So I signed up for an account and decided to make a simple bot in nodejs.

So after two weeks of development this is what I have to say.

I'm not going to go deep into how it's made, just how we use it.

The model is `text-davinci-003`.

---

So I set up the first bot, called Arc.

We started by asking it questions.

![](https://i.imgur.com/zHeo8pr.jpg)

Checking its logic. We found it good but also found it can contradict itself.

Some information was straight up incorrect.

---

Playing a bit with it more.

![](https://i.imgur.com/6pi0Zux.jpg)

---

Checked its multi-language capabilities

![](https://i.imgur.com/aS60bHL.jpg)

---

Then this is when it got really fun.

I set up another bot called Rupert.

Rupert was meant to have a specific personality.

Specifically: `Please respond in the style of Stewie from Family Guy`.

That was prepended before every prompt.

![](https://i.imgur.com/Vs5O1O3.jpg)

---

We found it was really easy to change the personality.

All it needs are simple instructions.

![](https://i.imgur.com/pcsfMAr.jpg)

---

Realized having hardcoded instructions or 
telling it how to act everytime was not flexible/easy enough.

So I decided to add commands to the bots.

![](https://i.imgur.com/pgBYWUU.jpg)

![](https://i.imgur.com/xXlvdSF.jpg)

![](https://i.imgur.com/ecroNHt.jpg)

Here's The Undertaker:

![](https://i.imgur.com/W7XIhgf.jpg)

---

Currently it has these commands:

![](https://i.imgur.com/66ufytw.jpg)

`!ur` is a shortcut to set a personality.

It changes the bot's `rules`. Which are prepended before every prompt.

You just do `bot: !ur an angry duck`

It's a shortcut to set the rules to:

`Respond as if you were an angry duck` 

Or you can use the `!rules` command and set something directly.

It has `users` and `admins`.

Admins can run all the commands.

The purpose of `users` is if you want to whitelist access to the bot.

It defaults to allowing everyone to ask and modify the bot's personality.

You can change those two permissions through commands.

---

Every prompt is standalone, there is no context/history.

This makes the bot cheaper to use. And maybe less confusing.

But sometimes you want some context. 

So I added a way to reference the previous message.

![](https://i.imgur.com/jarl405.jpg)

Just use `^` at the start of the message.

---

airc is open source: https://github.com/madprops/airc

---

So yes, we have Arc as the vanilla ai consultant for serious questions.

And we have Rupert to program it to act as anything!

It's been actually really fun.

![](https://i.imgur.com/gCTy8hF.jpg)
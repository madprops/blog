# Mall Code

![](mallcode.png)

Mall Code is a multiuser system for morse code communication.

Every user is in a zone at a certain speed (1 through 9).

For instance a user can be in `G1` which is the slowest zone.

Or `G9` which is the fastest zone.

Zones can be any letter from `A` to `Z`.

The faster zones are closer to the real normal morse code speed.

The slower zones are for newbies.

The speed of the zones determine the delays that consider the input a letter or word.

---

The only input accepted in the system is a single signal which is either a dot or a dash. This can be any keyboard signal or mouse button.

The `HUD` contains a button to toggle beep sounds, an indicator with the current zone name, and the number of users connected to that particular zone.

On the left there are the last 10 nouns typed in that zone. Which are words that are at least 3 chars in length that exist in the word list.

New words are added to the bottom of the vertical list.

---

The current letter formed by users is shown in white, and after another delay, the composed word is shown in yellow.

---

There is a 3 second lock for users to not be interrupted, by taking control of the morse code input, 3 seconds after the last signal sent. During this period users can't control the morse code input. After the lock is over, any user can start using it.

---

Each zone has a unique color theme (might be repeated).

Each user has a unique beep sound and color (might be repeated).

---

The default zone changes daily, based on a random generator that uses the current date as the seed.

The default zone is always of speed 3.

---

All the logic is handled in the server.

All clients can do is send `UP` and `DOWN` signals.

And efforts are made to avoid spam.

---

The name of the user that is currently talking is displayed on the top left center.

There is a zone dial on the top right to select the letter and speed.

---

Spam is punished with ip-based 60-second block times.

A user can have continued control for up to 60 seconds.

After that they lose control and get blocked for 10 seconds.

---

The username is based on a cookie created on first visit.

The name, color, and sound of users, are based on the username.

---

https://mall.merkoba.com/

https://github.com/madprops/mallcode
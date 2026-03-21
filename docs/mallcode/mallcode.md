# Mall Code

![](mallcode.png)

Mall Code is a multiplayer game for morse code communication.

Every player is in a zone at a certain speed (1 through 9).

For instance a player can be in `G1` which is the slowest zone.

Or `G9` which is the fastest zone.

Zones can be any letter from `A` to `Z`.

The faster zones are closer to the real normal morse code speed.

The slower zones are for newbies.

The speed of the zones determine the delays that consider the input a letter or word.

---

The only input accepted in the game is a single signal which is either a dot or a dash. This can be any keyboard signal or mouse button.

The `HUD` contains a button to toggle beep sounds, an indicator with the current zone name, and the number of players connected to that particular zone.

On the left there are the last 10 nouns typed in that zone. Which are words that are at least 3 chars in length that exist in a nouns list.

---

The current letter formed by players is shown in white, and after another delay, the composed word is shown in yellow.

---

There is a 3 second lock for players to not be interrupted, by taking control of the morse code input, 3 seconds after the last signal sent. During this period players can't control the morse code input. After the lock is over, any player can start using it.

---

Each zone has a unique color theme (might be repeated).

Each zone has a unique beep sound (might be repeated).

---

The default zone changes daily, based on a random generator that uses the current date as the seed.

---

https://mall.merkoba.com/

https://github.com/madprops/mallcode
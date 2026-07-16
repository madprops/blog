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

There is a button to change the dash from being slightly above the dots, slightly below, or on the same line.

There is a button to toggle animation effects on or off.

There is an About button.

---

If single letter, instead of printing a single letter word, the visible letter just changes color.

---

There is an update section with join and leave messages.

---

The URL contains a &zone parameter that is used to join specific zones and is updated automatically.

---

Certain words get to be displayed in a Bluesky account.

---

Sekrit zones can be reached by typing sekrit words.

Going to a sekrit zone unlocks it, places it on the map.

Using the map is possible to go back to the visited sekrit zones.

---

There's an anti-spam system.

---

There are echoes created through markov using the zone's words.

---

There are anomalies that exist temporarily, created at a certain % chance on every word.

---

Each letter sets the background color. All B zones are of a certain color, etc.

Sekrit zones and anomalies get a random color based on the zone name.

---

There is a bundler to automatically bundle js main and lib bundles.

---

The zone map icon goes red when locked (channel being used), and green when unlocked.

The rings around the zone map icon denote connection to the server.

---

The zone last activity only gets updated on word matches.

---

There are enemies called 'jammers' that spawn on a zone at 10% chance on words.

They can be attacked with `boom, pulse, shock, flare, crash`.

Every attack randomly does a 10 to 100 hp damage.

Jammers start with 100 hp. And they heal 25 hp on non jammer words.

When the hp goes to 0 the jammer gets destroyed.

This is shown in the top right log messages window.

---

https://mall.merkoba.com/

---

# Theories

`Mall Code` is a high effort and low throughput communication system.

In other words, there is effort and time required to produce a message.

Since time is part of the equation, any letter or word sent will need the appropriate durations, gaps, delays, to make it through. It won't be sent in milliseconds like with normal text chat systems.

This means that even if a tuner installs an extension to type the morse code for them or use a program to do this automatically, time will still be involved. Bots wouldn't be able to send or read thousands of words in seconds, instead they read one word.

---

The morse code communication allows tuners to show their skill level.

Skilled tuners will type faster, with less errors. They could be found in the higher speed zones.

More skilled tuners can incorporate obscure characters apart from a-z to adorn their messages.

So `Mall Code` allows gauging cognitive abilities while simply engaging in communication.

For instance you might want to sign your message with a nice name like:

![](server/img/mad.png)

---

Being a harder and slower mode of communication filters out types of communication tuners might not desire at that point, like low effort hate, violence, confusion, hostility, or time-wasting messages.

And it gives cleanly produced words more weight and meaning.

---

Connecting this to a social media system, like `Bluesky`, allows tuners to broadcast messages that could have meaning to other tuners.

Not all words are broadcasted, to avoid allowing tuners from sending problematic words, instead some words are manually whitelisted by adding them to a text file.

![](server/img/posts_2.png)

The posts have 2 components to consider, the code word, and the zone.

It can be a call to gather at that specific zone for a meeting.

Or it could be a codeword only members of an organized community can understand.

Or it can just be random, maybe funny, meaningless manifestations of life.

---

Banning this system would be absurd since it's banning one of the slowest and hardest forms of human communication. It would make it clear a state is desperate and has no regard for its citizens.

---

It can be used as an interface to access or create things.

For instance, it can be programmed so that certain words or sequences open doors, unlock computers, play messages, or any other action available.

There is already a system to register actions easily.

It is a semi-secure interface since it's not really concealed, it just requires some morse code skill and knowing certain keywords.

The keywords can be zone dependent, so for instance opening doors can only work if you are in the K4 zone.

It can be a way to provide an interface to fullfill wishes while having a certain friction, to not making it entirely easy to trigger actions, as a way to regulate actions.

---

If connected to a universal system, organizations can listen to specific zones for messages. For instance they might be interested in `SOS` messages, either on certain zones or globally. Maybe to provide assistance.

---

Special hardware can allow tuners to send morse code messages. For instance, a tuner might have a special network-enabled pen, or any object they can tap, and send something specific, maybe to a certain zone. This can be useful in emergency scenarios.

---

Since time is involved, this can't be easily used for computer-to-computer communication. Computers can send messages to each other in big volumes, very quickly. But in this system they would be subjected to the same constraints humans have. So either computers would have to end behaving more human here, or there would be no computers, making it a human-mostly network.

---

Streams and poll systems can use this as a way to gauge for support on certain things or events.

For instance they could check the `Bluesky` posts to check for codewords that would be relevant in the moment.

Streamers and organizations could start taking over some zones, or become associated with them.

---

This can be connected to an `imaginarium` to build structures in zones.

For instance if a tuner is able to write `cemetery` in `K6`, then an AI system would build a cemetery 3D structure in that zone in some sort of walkable video game, maybe a `VR` experience.

This allows tuners to have a say into what exists or what is happening in certain zones, limited by their initiative, and being able to write the words in time.

A tuner might be able to tap `coke` in the zone, making them now eligible to receive a nice cold `coca cola` drink.

---

Can be used for security purposes. Each zone meaning a certain room or event.

Participants use the beeps as pings or signals. And the words would have meaning:

For instance typing "hot" in M9 might mean something is happening there.

---

Our taps could be considered to be connected and felt by forces we can't see all the time.

`Morse Code` itself, being an old tech by now, could have found its way into systems that are actively listening.

Doing and `SOS` on a surface, without any tech, might trigger a vessel to appear in the sky.

Same with names of people you might know.

So I'd advice treating those with some sort of measure.

Now consider what that means in an online multi-user morse code system.

---

The unlockable zones make the system more exciting.

Once a tuner inputs a secret word they unlock a special zone.

These will remain unlocked and available at the `Zone Map`.

It provides discoverability and the creation of small communities.

![](server/img/zones.png)

---

The skill ceiling is high.

Fast morse code typers could be found in the high speed zones (7, 8, 9).

Tuners who are learning or practicing could start on slower speed zones.

This allows tuners to engage in zones with people of their current skill level.

Learners can observe high speed tuners talk among each other while rarely interacting.

This also allows high speed tuners to go to slower zones to help people sharpen their skill.

---

`Morse Code` is heavily based on sound.

Witnessing other skilled tuners, listening to how they form the words, can help tuners solidify their morse code skills.

Each tuner has a semi-unique name, color, and sound. It gives them some personality.

So on group conversations, it's easier to know who's currently talking.

---

The sekrit zones allow exclusive groups to be formed.

Depending on the word, people can arrive there randomly or by having the code shared to them.

This could be used in commercial systems where having access to certain zones unlocks services and menus in the establishment.

And there's always some effort to unlock the zones, some morse code must be performed.

---

Trying to hack and patch this for sport can be part of the fun.

Finding ways to automate messages without doing morse code / effort (cheating).

And detecting and understanding the exploits to patch them.

---

The combat mechanic to fight jammers adds another target to practice morse code.

This can be expanded more.
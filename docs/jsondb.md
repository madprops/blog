# JsonDB

My chat site is probably the biggest project I've worked on. Started working on it at around 2017.

It's made 100% in javascript. NodeJS for the server. Websockets. 100% vanilla, no frontend frameworks.

I bring it up because it doesn't use a database at all.

When I first started developing it I decided for some reason to use MongoDB.

I worked myself around mongo, adding various type checks. But it was a pain.

It was a pain because on mongo version upgrades the api changed.

So I had to rewrite parts of the backend to work again with the database.

Then there were plain corruptions. Ended up in a state where I couldn't use the data anymore.

In one ocassion I had to trigger a rollback on my vps, which took a while, just to recover mongo data.

At some point I decided I had enough.

But instead of simply changing the DB to something like Postgres, I made my own.

I made a fairly simple engine to save all data in a series of json files.

The structure was already there, since mongo were a bunch of "documents".

Each chat room has 1 document, and everything resides in there, including the last 500 messages.

Each user has 1 document and everything about it resides in there.

All these documents reside in a `db` directory.

![](https://i.imgur.com/cSkCZCv.jpg)

These are all plain json files.

The engine files look like:

![](https://i.imgur.com/tEsYwND.jpg)

One of the functions looks like:

![](https://i.imgur.com/5B91WX1.jpg)

The engine has some debouncer mechanisms to rate limit the file saves to be easy on the i/o.

There's a shared `manager` that performs some operations.

Rooms and users have apis to retrieve and update:

![](https://i.imgur.com/P4IMo1c.jpg)

I have mechanisms that allow me to write and maintain a schema:

![](https://i.imgur.com/ojflW7C.jpg)

These are the benefits:

1) I depend on nothing, I don't need to install, configure, or upgrade a 3rd party database.

1) All the data exists in the file system, and it's easy to inspect, edit, and backup.

1) I fully control it, can optimize and add what I need.

1) Installing the chat system becomes a lot simpler.
# Prompt Protocol

Imagine if there was a protocol that operating systems, browsers, an AI providers would understand to be able to open prompt links.

For example:

prompt://what+are+ants

This could be a clickable element in browsers or applications, similar to a URL.

When clicked it uses the configured AI provider to automatically open a new conversation and run that prompt.

So instead of telling people "ask your AI what ants are", you send them a link they can just click and it will open the configured AI provider for the request.

The OS or browser could have a chapter to allow the user to specify "their AI".

AI companies would need to get on board so they add special URLs or signals to allow this. Maybe through a browser extension or native mechanism to send AJAX signals to existing clients.

I might already have a Gemini tab open in Firefox. If I click a prompt link, I would expect that tab to be reused and simply see the new conversation popup with the new prompt now ongoing, instead of opening a new tab.

So browsers would need to be smart about this too, to know when an AI provider tab is already open and re-use it, focus it. Or just open a new tab, window, or application.

I think this makes sense because when URLs are shared it's to show a person something, when you try to tell a person "just ask your ai what x thing means" you want them to see something, might as well make it painless.

Prompt URL generators could be baked into the browsers, OS, applications. For instance click a button, write the prompt you want to share, get the prompt URL back ready copy, maybe URL shortener services for this might be created.
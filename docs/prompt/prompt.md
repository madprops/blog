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

For very long prompts services/domains/shorteners will have to be used because prompt links would get huge. But they can work based on the protocol itself, and applications can send prompt links internally between them and understand them.

---

## Proposed AI Prompt Protocol (`prompt://`) extensions

While the core `prompt://[query]` handles immediate text execution, the protocol requires extensions to support complex workflows, large context windows, and multimodal attachments without breaking URI constraints.

### 1. Staged Execution and the `wait` Parameter

To bypass the complexities of handling file streams or cross-origin issues in the URL bar, the protocol supports an execution flag. This shifts attachment handling back to the provider's UI.

* **Immediate Execution (Default):** `prompt://What+are+ants`
The handler wakes the AI provider, injects the text, and submits the prompt automatically.
* **Staged Execution:** `prompt://Analyze+this+diagram&wait=true`
The handler opens the provider, pre-fills the text area, but leaves the input focused and unsubmitted. This allows the user to manually drag-and-drop local attachments (images, PDFs) or edit the text before hitting Enter, mirroring the behavior of a `mailto:` link.

### 2. Remote Payloads and Prompt Shorteners

Standard URLs have a practical limit of around 2,000 characters, making massive prompts unshareable via direct strings. To solve this, the protocol supports fetching remote payloads.

* **Syntax:** `prompt://fetch?url=[https://domain.com/shared-prompt-id]`
* **Mechanism:** Instead of passing the prompt text directly in the URI, the handler instructs the AI provider's client to perform a GET request to the provided URL.

### 3. Remote Payload Data Structure

When using the `fetch` syntax, the remote service returns a standardized JSON envelope. This solves both the character limit and the automated attachment problem, allowing developers to programmatically share multimodal context.

The AI provider reads the JSON, pulls in any external media to its own cache, populates the input, and respects the execution flag.

**Example JSON Schema:**

```json
{
  "version": "1.0",
  "text": "Please analyze this server configuration and the attached network diagram.",
  "execute_immediately": false,
  "attachments": [
    {
      "type": "image/png",
      "url": "https://example.com/assets/network-diagram.png"
    },
    {
      "type": "text/plain",
      "url": "https://example.com/assets/config.txt"
    }
  ]
}

```
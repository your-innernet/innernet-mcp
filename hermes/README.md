# innernet for Hermes Agent

the memory your AI tools share. innernet keeps one versioned memory for every
project you work on and for you, and every tool you connect (Claude, ChatGPT,
Cursor, Grok, Hermes, any MCP client) reads and writes that same memory. what
you decide in one of them, the next one knows.

this package brings that memory into Hermes: the innernet MCP server and two
skills, `innernet:innernet` (find the project, load it, answer from what
matters, save decisions back) and `innernet:innernet-handoff` (where you left
off, and a note for the next session).

## install

```
hermes plugins install innernet
```

then turn on the sign-in. a portable package cannot ask for OAuth on its own,
so add the server to `~/.hermes/config.yaml` under `mcp_servers` (an entry
there wins over the package's own copy):

```yaml
mcp_servers:
  innernet:
    url: "https://innernet.live/api/mcp"
    auth: oauth
```

and sign in once:

```
hermes mcp login innernet
```

your browser opens innernet's own sign-in page. you need a free account at
[innernet.live](https://innernet.live). never paste an api key into a chat:
the sign-in handles it, and Hermes keeps and refreshes the token.

try: "load my innernet project context", "what did we decide about pricing?
check innernet", "where did I leave off?", "hand off: save my progress".

## what it does, plainly

- hosted only. the package is configuration and two markdown skills: no
  scripts, hooks, background processes, telemetry or self-update.
- every tool call goes to one place, `https://innernet.live/api/mcp`. Hermes
  sends what a call carries (a project name, your question, or the text you
  ask it to save) and innernet returns what your memory holds. innernet never
  reads Hermes's own memory, sessions or files.
- some tools write: saving context, capturing a note, writing a handoff,
  updating a task, forgetting something you ask it to forget. every write lands
  in your innernet account, versioned, and you can read, edit or delete it on
  your dashboard.
- personal memory is gated by the disclosure levels you set; private facts are
  never returned to an AI.
- inside innernet, a few model providers do work on what you saved (named in
  the privacy policy): https://innernet.live/privacy · terms:
  https://innernet.live/terms

every app innernet works in, with the shortest way into each:
https://innernet.live/docs/everywhere

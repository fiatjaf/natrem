natrem
======

Natrem (silly name that means "Native Remote") is a protocol for modern internet apps.

We call them "internet apps" and not "web apps" because the "web" is terminantly associated with browsers, and the idea here is to replace browsers.

Natrem defines a set of smart, interactive components that a _client_ must implement and a _server_ can specify in its messages to this _client_, such that the _client_ can then render a native interface the _user_ can then use to interact with the _server_.

The server is just some normal Websocket server, reacheable and identified by a domain name. The _client_ opens a Websocket to this server and it sends messages to the client that what the _client_ is supposed to show to the _user_.

## For example,

a user could open its _client_ and type the URL of some Natrem-capable server in its URL box, say, `natrem:echoservice.com`, then the client will open a Websocket connection to `wss://echoservice.com/natrem`.

The _server_, upon connection, may send a message that says

```json
[
  ["inputbutton", {"label": "ib1"}]
]
```

Upon seeing this, the _client_ will render an input box and a button. The button will say something default, like "OK"; then the _user_ will type "something" on that box and click to send (or press Enter); the client will then send

```json
{
  "ib1": "something"
}
```

Finally, the server will see that message and reply with

```json
[
  ["text", "You wrote 'something'."]
]
```

Which will cause the _client_ to render a text view with these contents written in it.

### Why this?

Because web browsers are not the best way to serve simple applications that interact with a server. Web applications, as they are called, are hard to write, take a long time to be finished, even when they are very simple, and the result is a heavy, slow program that infects users' computers with unwanted arbitrary code, and in the meantime the push for more and more functionality turns browsers into enormously bloated machines full of bugs that no one can implement from scratch ever again so we're left with only Chrome.

In other words, ["the web is unimplementable"](https://twitter.com/__anp__/status/1117828315715260416).

### Are you reinventing browsers?

Yes and no. Yes in the sense that browsers are also just-in-time renderers of stuff servers send to them. No in the sense that these clients are simple enough for anyone to implement, they're safe, fast, and come with interactive components out-of-the-box -- differently from browsers, in which a simple button that you can click and it will change something in the screen or make a request to a server can take hours to be written and many megabytes of JavaScript dependencies.

### But then Natrem clients will be very limited in functionality

Yes, and that is a good thing. If an application wants to be very flexible it shouldn't be using Natrem -- or browsers! --, it should be written as a fully native application and people should install them.

### If this is going to replace web browsers, where are we going to read stuff from the internet?

Maybe browsers will become again what they were created to be. Or we will transition to something like https://gemini.circumlunar.space/ for these use cases.

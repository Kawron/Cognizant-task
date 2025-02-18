# Readme

Karol Wrona

## Task 1

Quick note: I used python threads for this example which is fine, however in more complex scenario I would use library like Celery. Also the source code contained a bug in its original form, the variable *next_task_id* was referenced before global keyword.

## Task 2

First, I would like to point that the fact of using RxJs on the frontend is not saying anything about how the backend api should be designed. For example, in Angular framework, the standard pattern is to wrap every http request in Observable, no matter if this is a stream of data or a single value. And the functionality of server side updates could be done without using RxJs (not saying that it is a good idea. I'm personally a big fan of RxJs).
So, to send events from backend we can use a couple of options:
- websockets
- server side events
- pooling
- in some scenario we can use Push API (https://developer.mozilla.org/en-US/docs/Web/API/Push_API)

Let's start with the pooling, it is the easiest and the least effective form of doing this so we won't use it. Push Api can be an interesting choice in some scenario as it doesn't require the web application to be opened, but it requires user agreement to send notifications. SSE and websockets seems to be the best options, so let's compare them. Websocket offers two-way communication and supports binary data, websocket can be implemented in python using Flask-SocketIO library. SSE offers only one way connection, and it doesn't work well with binary, however it is overall simpler to implement and for our case it is sufficient. To implement SSE we can use library called Flask-SSE or just use plain Flask. Also, we should consider how these events are created and handled on the server side. For this we can use Flask Signals api (using Blinker library) or even RxPY.

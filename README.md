server sent events with Play
============================

Launch the code:

    ./activator ~run

This project expose 2 type of ways to generate SSE:

 * **WORKS** `http://locahost:9000/ticks` shoots texts via `Source.tick`
 * **FAILS** `http://localhost:9000/actor-flow` shoots two messages via a akkastream Source.actorRef


Check with curl:

    octomaa:tmp alex$  curl  -H "Accept: text/event-stream" http://localhost:9000/ticks
    data: TICK
    
    data: TICK
    
    data: TICK
    ^C
    
    
    octomaa:tmp alex$  curl  -H "Accept: text/event-stream" http://localhost:9000/actor-flow
    ^C    

**Problem** : The second method sees the messages going through the akkastream flow but are not sent through the http channel...

 All the code is in `app/controllers/StreamController`
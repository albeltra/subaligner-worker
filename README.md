# subaligner-worker
This repo contains instructions for building a rq worker for [subaligner](https://github.com/baxtree/subaligner)
built on my own [fork](https://github.com/albeltra/subaligner-trained) including my personally trained model.
Despite being based on alpine, the image is ~2.5 Gb since subaligner requires 
several scientific python libraries and ffmpeg.

Prerequisites: A running redis server.

### Running the Container
You can build the image yourself: <br>
```
git clone https://github.com/albeltra/subaligner-worker --recrusive
cd subaligner-worker
docker build -t subaligner-worker .
```
Then run it using your freshly built image or mine. At minimum you must properly
map your media directories and specify the host and port of your redis instance:

```
docker run \
       -v /movies:/movies \
       -v /tv:/tv \
       -e REDIS_HOST=<IP OR HOST NAME> \
       -e REDIS_PORT=<PORT> \
       beltranalex928/subaligner-worker \
```

### Start the WSGI Server
Be sure to setup the companion WSGI server to start launching jobs. Check out the 
instructions [here](https://github.com/albeltra/subaligner-wsgi)
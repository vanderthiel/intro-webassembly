# intro-webassembly

Our community - Front-End - organizes events regularly.

This is the talk "Introducing WebAssembly" on March 8, 2022 for [Frontend Lightning Talks - WebAssembly](https://www.meetup.com/sogeti-frontend/events/282711845/).

Here you can find the demos, for which I can't take credit myself. The original is from [Surma](https://twitter.com/dassurma) written in 2018: [Emscripting a C library to Wasm](https://developers.google.com/web/updates/2018/03/emscripting-a-c-library).

## Preparation

1. Clone this repository.
1. Pull in the docker image for the emscriptem compiler:
`docker pull trzeci/emscripten`.
1. (optional) Install http-server for node for a simple webserver:
`npm install http-server -g`

Make sure to disable browser cache when doing both demos, as the wasm file tends to get cached by the browser.

## Demo 1 - Fibonacci

Go to directory `fib`.

Run the Emscriptem compiler from docker:
``` bash
docker run --rm -v $(pwd):/src trzeci/emscripten emcc -O3 -s WASM=1 -s EXTRA_EXPORTED_RUNTIME_METHODS='["cwrap"]' fib.c
```

Now start a webserver from this directory:
`http-server`

## Demo 2 - webp library in WebAssembly

Go to directory `webp`.

We will use the [webp library from github](https://github.com/webmproject/libwebp):
`git clone https://github.com/webmproject/libwebp`.

Run the Emscriptem compiler from docker:
``` bash
docker run --rm -v $(pwd):/src trzeci/emscripten emcc -O3 -s WASM=1 -s EXTRA_EXPORTED_RUNTIME_METHODS='["cwrap"]' -s ALLOW_MEMORY_GROWTH=1 -I libwebp webp.c libwebp/src/{dec,dsp,demux,enc,mux,utils}/*.c
```

Now start a webserver from this directory:
`http-server`

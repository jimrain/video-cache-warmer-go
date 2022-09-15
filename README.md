# HLS cache warmer for Go

This is my first attempt at a Go C@E applicaiton. Since my first Rust app was a video cache warmer I decided to reproduce it in Go.

## Go Features

* HLS manifest parsing using the Go m3u8 package.
* Go routines to asychronously make head requests for media files.
* Wait Groups to make sure I'm done sending my requests before the app ends

## Understanding the code

When a request comes in to the applicaiton it forwards it to the backend intact. It then checks to see if the request has an .meu8 extension. If it does the Go HLS library is used to parse the manifest. If it's the master manifest it's just passed through. If it's a playlist manifest it takes the first 5 segments and makes head requests for each of them.

In the code there is some url manipulation. This is because the manifest contains relative urls and we have to make them absolute.

## Demoing this application.

It is reccomended to use the [Fastly CLI](https://github.com/fastly/cli) for this template. The template uses the `fastly.toml` scripts, to allow for building the project using your installed TinyGo compiler. The Fastly CLI should also be used for serving and testing your build output, as well as deploying your finalized package!

## Security issues

Please see our [SECURITY.md](SECURITY.md) for guidance on reporting security-related issues.

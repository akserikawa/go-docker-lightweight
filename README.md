# Minimal Docker containers for Go applications

This repo features a simple demo app that fetches https://google.com and outputs the status code and the size of the html in the response body.

## Usage
Clone this repo.

To be able to make requests via https, copy the ssl certificates from your host machine and paste them in the current directory.
    
> For many Linux distributions, this file is in `/etc/ssl/certs/ca-certificates.crt`. In my case, I've got mac OSX with openssl installed via homebrew, so this file was in `/usr/local/etc/openssl/cert.pem`).

Build the main.go file by running:

    CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

We’re disabling cgo which gives us a static binary. We’re also setting the OS to Linux (in case someone builds this on a Mac or Windows) and the `-a` flag means to rebuild all the packages we’re using, which means all the imports will be rebuilt with cgo disabled.

Build the image
    
    $ docker build -t golang-lightweight-image .

Run the following command to see the output in your terminal

    $ docker run -it --rm golang-lightweight-image

> Note: the `--rm` will delete the container when the app exits.

That's it! :)
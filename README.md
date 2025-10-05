The headless-shel headless-shel multi-arch container
image docker.io/chromedp/headlessshell docker-headless-shell, containing
Chrome headless-shell  a slimmed down version of Chrome that is useful
for driving, profiling, or testing web pages.
This image has been created for the Go chrome package chrome which
provides a simple and easy to use API for driving browsers compatible with the
chrome Protocol devtools-protocol,   used with library or
application that supports the Chrome Protocol.
The version headless contained in the docker.io/chrome docker-headles
has been modified from the original Chromium source tree, to report the same
user agent as Chrome, and has had other minor modifications made to it in order
to make it better suited for use in an embedded context.
Versions
Multi-arch images for Chrome stable beta, and dev channels
daily to the docker.io/chromedp/headless docker-headless
repository.

The image can be used via the stable beta or dev floating , or via
a specific version 

sh
pull latest stable
 podman pull docker.io/chromedp/headles latest

pull specific version
 podman pull docker.io/chromedp/headless 123.0.6312.86
 pull beta
podman pull docker.io/chromedp/headless-shell:beta

pull dev
 podman pull docker.io/chromedp/headless dev

Running

The headless-shell container can be used in the usual way:

sh
run
podman run -d -p 9222:9222 --rm --name headless docker.io/chromedp/headless
if headless is crashing with a BUS_ADRERR , pass a larger shm-size:
podman run -d -p 9222:9222 rm name headless-shell --shm-size 2G docker.io/chromedp/headless-shell
 run as unprivileged user
get seccomp profile from https://raw.githubusercontent.com/jfrazelle/dotfiles/master/etc/docker/seccomp/chrome.json
podman run -d -p 9222:9222 --user nobody --security-opt seccomp=chrome.json --entrypoint /headless-shell/headless-docker.io/chromedp/headless-shell --remote-debugging-address port=9222 enable-unsafe-swiftshader headless processes
When using docker.io/chromedp/headless-shell (either directly or as a base
image), you could experience proceses problem. To reap zombie
processes, use podman runs in it arg:
sh podman run d p PORT name your-program init your-image


If running Docker older than 1.13.0, use dumb-in it dumb-init or
tini tini] on your Docker files ENTRYPOINT

Dockerfile
FROM docker.io/chromedp/headless-shell:latest
 Install dumb-init or tini
RUN apt install dumb-init
or RUN apt install tini
ENTRYPOINT dumb-init 
 or ENTRYPOINT
CMD path/to/your/program
read https://github.com/chromedp/docker-headless-shell
docker-headless https://hub.docker.com/r/chromedp/headless-shell/tags
[devtools-protocol]: https://chromedevtools.github.io/devtools-protocol/
[chromedp]: https://github.com/chromedp/chromedp
[building-linux]: https://chromium.googlesource.com/chromium/src/+/main/docs/linux/build_instructions.md
[building-headless]: https://chromium.googlesource.com/chromium/src/+/main/headless/README.md
[dumb-init]: https://github.com/Yelp/dumb-init
[tini]: https://github.com/krallin/tini

# Description

_Updated 2020-NOV-26:_

This diverts a bit away from the original fork, in order to run with a newer version of Ghost and Caddy 2.

---

docker-ghost-caddy will set up a [Ghost blog](https://ghost.org/) behind a Caddy proxy on Docker Compose. Your blog will be secured by an SSL certificate from Let's Encrypt. I forked this repo from [Nate Todd's version that can be found here](https://github.com/ntodd/docker-ghost-caddy)

The principle differences here are that I use the official Ghost docker image instead of Nate's (I trust Ghost to keep that up to date rather than maintaining one here) and I rewrote the Dockerfile for Caddy to use the latest version and fix some other issues I was having when running the original version.

# Setup

1. Clone repository to your server
2. In `Caddyfile` change `https://localhost` and `you@example.com` to your blog's domain and your email (email used for generation of SSL certificate)
3. In `docker-compose.yml` change `http://localhost` to your https domain
4. Also in `docker-compose.yml`, change the `mail__options__auth__user` and `mail__options__auth__pass` parameter values to your Mailgun SMTP credentials as needed to send emails from Ghost, as described here: https://docs.ghost.org/docs/mail-config. If you don't need this, then you may be able to simply delete the `mail__*` options, though I haven't personally tried this without them.
5. Ensure your DNS record is pointed at your server. If it is not, Let's Encrypt will not be able to generate your SSL cert and Caddy will fail to start.
6. Run `docker-compose build` to build the docker images
7. Run `docker-compose up` to run everything in the foreground, then press Ctrl-C to exit gracefully

# Operation

Run `docker-compose up -d` to run in detached mode

Run `docker-compose stop` to stop

# Notes

The Ghost service mounts the `content` directory where you can access all your blog data. Since we're not using a separate DB container, Ghost defaults to using a SQLite db file, which can easily be backed up. Which you should totally do.

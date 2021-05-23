# Caddyconf

[Caddy](https://caddyserver.com) configurations for quickly setting up static websites on a box. There's no magic here, the main configuration file is [Caddyfile](Caddyfile.example).

This uses a simple to read DSL so you don't need to figure out what options and configurations you need. The DSL is defined in the [caddyinc/lib](caddyinc/lib)

**Supported Caddy Version: V2.x**

## Why

I made this to make my life easier spinning static websites, all I need to do is spin a DigitalOcean box with Caddy on with this configuration setup then occasionally rsync my static website build to the server in the right locations.

So if this doesn't quite work for you, modify it at your own leisure, PRs are also welcomed. This is offered under the MIT license.


## How to use

I suggest you take a glance at [Caddy's Documentation](https://caddyserver.com/docs/) as a first step.

As show cased in the example Caddyfile, first thing you'd want to do is to import the lib. Easily enough

```
import caddyinc/lib
```

Then tell Caddy what domain names you'd like to handle, then use the lib/* directives to
pull in the common functionality you need.

```
foobar.example.org {
  import lib/make_website foobar.example.org
}
```

Caddy automatically provisions an SSL certificate for you, to learn more about that please check [Caddy's Documentation](https://caddyserver.com/docs/)

### Assumptions

Some assumptions are made by the configurations defined in [caddyinc/lib](caddyinc/lib)

- You're using a static site generator, like [Hugo](https://gohugo.io) or others.
- Your site build directory contains an `error` directory with a file named `notfound.html` to catch 404s (the lib code automatically handles this for you)
- All directories referenced anywhere in the configurations are expected to be already present on the server
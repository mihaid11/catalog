# Node 22 Prisma Server

This directory contains a Node [`Prisma`](https://www.prisma.io/) implementation running on Unikraft.

## Set Up

To run this example, [install Unikraft's companion command-line toolchain `kraft`](https://unikraft.org/docs/cli), clone this repository and `cd` into this directory.

## Run and Use

Use `kraft` to run the image and start a Unikraft instance:

```bash
kraft run --rm -p 3000:3000 --plat qemu --arch x86_64 -M 1024M .
```

If the `--plat` argument is left out, it defaults to `qemu`.
If the `--arch` argument is left out, it defaults to your system's CPU architecture.

Once executed, it will open port `3000` and wait for connections.
To test it, you can use `curl`:

```bash
curl localhost:3000/feed
```

You should see a feed of blog posts in JSON format.

## Inspect and Close

To list information about the Unikraft instance, use:

```bash
kraft ps
```

```text
NAME             KERNEL                      ARGS                              CREATED       STATUS   MEM   PORTS                   PLAT
vigilant_kokomo  oci://unikraft.org/node:18  /usr/bin/node /usr/src/server.js  1 minute ago  running  488M  0.0.0.0:3000->3000/tcp  qemu/x86_64
```

The instance name is `vigilant_kokomo`.
To close the Unikraft instance, close the `kraft` process (e.g., via `Ctrl+c`) or run:

```bash
kraft rm vigilant_kokomo
```

Note that depending on how you modify this example your instance **may** need more memory to run.
To do so, use the `kraft run`'s `-M` flag, for example:

```bash
kraft run -p 3000:3000 --plat qemu --arch x86_64 -M 2048M .
```

## `kraft` and `sudo`

Mixing invocations of `kraft` and `sudo` can lead to unexpected behavior.
Read more about how to start `kraft` without `sudo` at [https://unikraft.org/sudoless](https://unikraft.org/sudoless).

## Learn More

- [How to run unikernels locally](https://unikraft.org/docs/cli/running)
- [Building `Dockerfile` Images with `BuildKit`](https://unikraft.org/guides/building-dockerfile-images-with-buildkit)

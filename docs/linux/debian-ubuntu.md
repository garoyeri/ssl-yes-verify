---
sidebar_position: 1
tags: [linux, debian, ubuntu, openssl, java]
---

# Debian, Ubuntu, and related Distributions

Most versions of Debian and Ubuntu (and their variants) are setup to follow the same process to update the certificates for OpenSSL. The tooling in the `ca-certificates` package will typically make `curl` and `wget` work, and when you plug in stuff like OpenJDK, it  ... should work too.

## Ubuntu 22.04

```docker
FROM ubuntu:22.04

COPY ["certs/*.crt", "/usr/local/share/ca-certificates/"]

RUN apt update && apt install -y curl wget ca-certificates && \
  apt autoremove && apt clean && \
  update-ca-certificates
```

## Debian Bullseye

```docker
FROM debian:bullseye

COPY ["certs/*.crt", "/usr/local/share/ca-certificates/"]

RUN apt update && apt install -y curl wget ca-certificates && \
  apt autoremove && apt clean && \
  update-ca-certificates
```

## Debian Stable

```docker
FROM debian:stable

COPY ["certs/*.crt", "/usr/local/share/ca-certificates/"]

RUN apt update && apt install -y curl wget ca-certificates && \
  apt autoremove && apt clean && \
  update-ca-certificates
```

## Referencing the CA List

Once the certificate list is updated, you can access the new list from here:

```
/etc/ssl/certs/ca-certificates.crt
```

## Java Support

The Debian and Ubuntu updates will automatically update a Java keystore as well. When you install the `openjdk-8-jdk` or the `openjdk-8-jre` packages (and likely other versions) then a script is added: `/etc/ca-certificates/update.d/jks-keystore` that updates a default keystore with the ultra-secret password `'changeit'`. This is OK because the certificate store is only writeable by `root` and it should only contain the public keys for certificate authorities which is all public information.

The updated JKS is stored in `/etc/ssl/certs/java/cacerts`. If you end up installing Java after you run `update-ca-certificates` you'll need to run it again manually to generate the `cacerts` JKS file. There doesn't seem to be a trigger that does it automatically.

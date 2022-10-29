---
slug: ubuntu
title: Ubuntu
authors: garoyeri
tags: [linux, ubuntu, openssl]
---

Most versions of Ubuntu are setup to follow the same process to update the certificates for OpenSSL. The tooling in the `ca-certificates` package will typically make `curl` and `wget` work, and when you plug in stuff like OpenJDK, it  ... should work too.

## Docker Example

```docker
FROM ubuntu:22.04

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

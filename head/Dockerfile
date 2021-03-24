# -*- mode: dockerfile; coding: utf-8 -*-
FROM schemers/bigloo AS build
RUN apt-get update && apt-get -y --no-install-recommends install \
      git ca-certificates \
      build-essential autoconf automake libtool m4 \
      libgmp-dev libpcre3-dev libssl-dev libunistring-dev \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /build
RUN git clone https://github.com/manuel-serrano/bigloo.git --depth 1 --tags
WORKDIR /build/bigloo
RUN ./configure
RUN LD_LIBRARY_PATH=/usr/local/lib/bigloo/4.4b \
      make bigboot BGLBUILDBINDIR=/usr/local/bin
RUN make install-progs
RUN make fullbootstrap-sans-log
RUN make install-sans-docs
RUN make fulltest

FROM debian:buster-slim
COPY --from=build /usr/local/ /usr/local/
CMD ["scheme-banner"]

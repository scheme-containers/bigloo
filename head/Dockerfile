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
RUN make
RUN make install

FROM debian:buster-slim
COPY --from=build /usr/local/ /usr/local/
CMD ["scheme-banner"]

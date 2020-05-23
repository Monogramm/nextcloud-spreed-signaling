# Modified from https://gitlab.com/powerpaul17/nc_talk_backend/-/blob/dcbb918d8716dad1eb72a889d1e6aa1e3a543641/docker/janus/Dockerfile
FROM alpine:3.11

RUN apk add --no-cache curl autoconf automake libtool pkgconf build-base \
  glib-dev libconfig-dev libnice-dev jansson-dev openssl-dev zlib libsrtp-dev \
  gengetopt libwebsockets-dev git

# usrsctp
RUN cd /tmp && \
    git clone https://github.com/sctplab/usrsctp && \
    cd usrsctp && \
    ./bootstrap && \
    ./configure --prefix=/usr && \
    make && make install

# JANUS

ARG JANUS_VERSION=0.9.2

WORKDIR /usr/src/janus

RUN mkdir -p /usr/src/janus && cd /usr/src/janus && curl -L https://github.com/meetecho/janus-gateway/archive/v$JANUS_VERSION.tar.gz | tar -xz

WORKDIR /usr/src/janus/janus-gateway-$JANUS_VERSION

RUN ./autogen.sh && ./configure --disable-rabbitmq --disable-mqtt --disable-boringssl && \
    make && make install && make configs

CMD [ "janus" ]

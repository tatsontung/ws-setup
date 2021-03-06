FROM node:alpine

LABEL name="node-alpine" \
      description="node image" \
      url="https://node-image" \
      maintainer="tatsontung@noreply.com"

# Install multiple packages :
RUN apk add --update --no-cache bash tzdata make gcc g++ python git tzdata nginx unzip openjdk8 && \
  rm -rf /tmp/* /var/cache/apk/*

# Install angular v2
RUN npm install -g \
    @angular/cli \
    karma \
    karma-chrome-launcher \
    --unsafe

# Install chromium
RUN apk -U --no-cache \
	--allow-untrusted add \
    zlib-dev \
    chromium \
    openjdk8 \
    xvfb \
    wait4ports \
    xorg-server \
    dbus \
    ttf-freefont \
    mesa-dri-swrast \
    grep \
    udev

# Minimize size
RUN rm -rf /var/lib/apt/lists/* \
    /var/cache/apk/* \
    /usr/share/man \
    /tmp/* \
    /usr/lib/node_modules/npm/man \
    /usr/lib/node_modules/npm/doc \
    /usr/lib/node_modules/npm/html \
    /usr/lib/node_modules/npm/scripts

ENV CHROME_BIN=/usr/bin/chromium-browser
ENV CHROME_PATH=/usr/lib/chromium/

# Update timezone and clean things
RUN cp /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN echo "Europe/Paris" >  /etc/timezone
RUN date
RUN apk del --no-cache tzdata

USER root
FROM resin/raspberrypi3-alpine-node:8

# Defines our working directory in container
RUN mkdir -p /usr/src/app/
WORKDIR /usr/src/app

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN apk add --no-cache make gcc g++ python git linux-headers py-rpigpio && \
  JOBS=MAX npm install -g --production --silent \
    node-red \
    node-red-contrib-influxdb \
    node-red-contrib-mapper \
    node-red-contrib-resinio \
    node-red-contrib-ttn \
    node-red-dashboard \
    node-red-node-serialport \
    && \
  apk del make gcc g++ linux-headers && \
  npm cache clean --force && rm -rf /tmp/*

COPY ./app ./
VOLUME /var/lib/node-red

EXPOSE 80

# server.js will run when container starts up on the device
CMD ["bash", "/usr/src/app/start.sh"]

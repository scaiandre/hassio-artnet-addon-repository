FROM node:12 AS base
WORKDIR /home/node/app

EXPOSE 6454/udp

ENV NODE_ENV=production

RUN git clone https://github.com/scaiandre/artnet-hue-entertainment.git

WORKDIR /home/node/app/artnet-hue-entertainment

RUN mkdir -p .config/artnet-hue-entertainment-nodejs && \
    ln -s /data/options.json .config/artnet-hue-entertainment-nodejs/config.json
RUN npm install

ENTRYPOINT ["node", "/home/node/app/artnet-hue-entertainment/build/cli.js", "run"]

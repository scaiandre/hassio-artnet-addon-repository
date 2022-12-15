FROM node:12 AS base
WORKDIR /home/node/app

EXPOSE 6454/udp

ENV NODE_ENV=production

RUN git clone https://github.com/scaiandre/artnet-hue-entertainment.git
RUN mkdir -p artnet-hue-entertainment/.config/artnet-hue-entertainment-nodejs
RUN ln -s /data/options.json artnet-hue-entertainment/.config/artnet-hue-entertainment-nodejs/config.json

ENTRYPOINT ["node", "/home/node/app/artnet-hue-entertainment/build/cli.js", "run"]

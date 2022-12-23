FROM node:15 AS base
WORKDIR /home/node/app

ENV NODE_ENV=production

RUN git clone https://github.com/scaiandre/artnet-hue-entertainment.git

WORKDIR /home/node/app/artnet-hue-entertainment

RUN git checkout "feature/homeassistant_squash"

RUN ln -s /data/options.json /home/node/app/artnet-hue-entertainment/config.json
RUN yarn install

ENTRYPOINT ["node", "/home/node/app/artnet-hue-entertainment/build/cli.js", "from-config"]

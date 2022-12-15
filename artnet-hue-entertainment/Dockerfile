FROM node:12 AS base
WORKDIR /home/node/app

EXPOSE 6454/udp

ENV NODE_ENV=production

RUN mkdir -p .config/artnet-hue-entertainment-nodejs
RUN ln -s /data/options.json .config/artnet-hue-entertainment-nodejs/config.json
RUN git clone https://github.com/scaiandre/artnet-hue-entertainment.git /home/node/app/

ENTRYPOINT ["node", "/home/node/app/build/cli.js", "run"]

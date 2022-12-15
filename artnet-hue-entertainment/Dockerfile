FROM node:12 AS base
WORKDIR /home/node/app

EXPOSE 6454/udp

ENV NODE_ENV=production

RUN git clone https://github.com/scaiandre/artnet-hue-entertainment.git .

ENTRYPOINT ["node", "/home/node/app/build/cli.js", "run"]

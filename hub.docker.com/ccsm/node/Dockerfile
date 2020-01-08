FROM node:6.4.0-slim

RUN apt-get update \
 && wget https://github.com/Yelp/dumb-init/releases/download/v1.0.2/dumb-init_1.0.2_amd64.deb \
 && dpkg -i dumb-init_*.deb \
 && rm dumb-init_*.deb

ENTRYPOINT ["dumb-init"]
CMD ["npm", "-q", "start"]
STOPSIGNAL SIGTERM

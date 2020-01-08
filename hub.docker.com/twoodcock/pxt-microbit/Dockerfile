FROM node:8-jessie

WORKDIR /

COPY pxt-microbit pxt-microbit

RUN cd pxt-microbit/ \
    && npm install -g pxt \
    && npm install 

EXPOSE 8080 3233

WORKDIR /pxt-microbit

ENTRYPOINT ["pxt", "serve", "-h", "0.0.0.0", "-p", "8080","--noBrowser"]
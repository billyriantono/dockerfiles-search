FROM node:latest
RUN npm install -g firebase-tools
WORKDIR /src
EXPOSE 9005
VOLUME /root/.config
VOLUME /src
ENTRYPOINT ["firebase"]

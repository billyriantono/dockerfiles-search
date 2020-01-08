FROM openjdk:8u201-jre-alpine

EXPOSE 25565
EXPOSE 80

WORKDIR /app
RUN apk --no-cache add nodejs nodejs-npm git && \
    git clone https://github.com/froadus/NodeMinecraft.git . && \
    npm install

ENV JAR=server.jar
ENV XMS=1024M
ENV XMX=2048M
ENV MC_FOLDER=/data
ENV WEB_PORT=80
ENV LOG_LENGTH=500
ENV USERNAME=admin
ENV PASSWORD=m8A9emS9Hnkz6PtG

WORKDIR /data
CMD ["node", "/app/minecraft.js"]
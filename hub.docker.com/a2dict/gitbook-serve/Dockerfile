FROM node:10

RUN mkdir /mdbook && mkdir /work
WORKDIR /work

RUN apt update && apt install -y openjdk-8-jre

RUN npm i -g gitbook-cli && \
    gitbook --version

COPY run.sh /run.sh
COPY build.sh /build.sh
RUN chmod +x /run.sh /build.sh
CMD [ "/run.sh" ]

EXPOSE 8080
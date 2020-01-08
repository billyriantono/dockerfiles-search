FROM node:latest

RUN npm install -g gitbook-cli && \
    npm install -g gitbook-plugin-mermaid && \
    npm install -g mermaid

RUN gitbook install

RUN apt-get clean autoclean && \
    npm cache clear && \
    rm -rf /tmp/* /var/lib/{apt,dpkg,cache,log}/*

WORKDIR /gitbook

RUN gitbook init

VOLUME /gitbook

EXPOSE 4000 35729

CMD ["gitbook", "serve", "/gitbook"]

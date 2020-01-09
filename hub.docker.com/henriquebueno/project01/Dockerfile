FROM henriquebueno/node_app01:1.7
EXPOSE 3000

RUN rm -rf /app

WORKDIR /app

RUN git clone https://hgbueno:36ctVZWByRpSf2bdKF6W@bitbucket.org/hgbueno/project01.git .

ENTRYPOINT ["node", "app.js"]

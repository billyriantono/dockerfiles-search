FROM alpine:3.9

WORKDIR /tmp

RUN apk add git npm ca-certificates wget jq
RUN wget https://github.com/bronze1man/yaml2json/releases/download/v1.3/yaml2json_linux_amd64 -O yaml2json -T 60 -w 10
RUN chmod -v a+x yaml2json
RUN mv -v yaml2json /usr/bin/
RUN npm install -g ajv-cli
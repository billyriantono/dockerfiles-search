FROM alpine:3.10

RUN apk add g++ python make npm

RUN npm i spdlog

CMD /bin/sh -c "node -p 'require(\"spdlog\")'"

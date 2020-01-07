FROM nginx:1.13-alpine

ENV TZ=Asia/Shanghai

RUN apk add --no-cache tzdata \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone

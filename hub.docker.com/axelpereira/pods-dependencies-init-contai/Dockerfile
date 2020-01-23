FROM alpine:3.7

RUN apk add --no-cache curl

run mkdir /app
COPY save_results.sh /app
WORKDIR /app

ENTRYPOINT ["sh","save_results.sh"]

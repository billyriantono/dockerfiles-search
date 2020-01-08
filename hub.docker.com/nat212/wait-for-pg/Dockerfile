FROM alpine:latest
WORKDIR /home
ADD wait.sh .
RUN apk add --no-cache postgresql-client bash
ENTRYPOINT ["bash", "wait.sh"]

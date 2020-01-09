FROM alpine:latest
MAINTAINER MrRobot
LABEL Description="This image is a little command line tool" Vendor="Evil Corp" Version="1.0"
RUN apk update && apk upgrade && apk add --no-cache nano tmux htop elinks
CMD ["tmux new-session -s EvilCorpBckUp && split-window -d  && htop"]
ENTRYPOINT ["bin/sh", "-c"]

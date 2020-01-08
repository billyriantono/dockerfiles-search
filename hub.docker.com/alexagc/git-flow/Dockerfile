FROM node:8.11.0-slim

LABEL maintainer="alexcanal@gmail.com"

RUN apt-get update && apt-get install -y git git-flow util-linux curl && apt-get clean

CMD [ "git-flow" ]

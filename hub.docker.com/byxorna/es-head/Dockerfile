FROM nginx:1.9
MAINTAINER Gabe Conradi <gummybearx@gmail.com>
ENV ES_HEAD_SHA 77e53bb74960db095902b5a32334421ecde0fc11
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*
WORKDIR /usr/share/nginx/html
RUN rm -rf * && \
  git clone https://github.com/mobz/elasticsearch-head.git . && \
  git reset --hard $ES_HEAD_SHA && \
  rm -rf .git
EXPOSE 80

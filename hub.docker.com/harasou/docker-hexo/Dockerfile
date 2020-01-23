FROM dockerfile/nodejs
MAINTAINER harasou

RUN \
  npm install hexo -g

ADD hexo-setup        /usr/local/bin/hexo-setup
ADD hexo-theme-apollo /usr/local/bin/hexo-theme-apollo

WORKDIR /data

EXPOSE 4000
CMD ["hexo","server","-i","0.0.0.0"]

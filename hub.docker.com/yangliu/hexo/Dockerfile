# use the node base image provided by official repo
FROM node:latest
MAINTAINER Yang Liu <istef.liu@gmail.com>

# prepare work directory
WORKDIR /hexo

# install hexo and hexo server
RUN \
    npm install hexo-cli -g \
    && npm install hexo-server -g

# replace this with your application's default port
EXPOSE 4000

# start bash for development
CMD ["/bin/bash"]
FROM node:latest
VOLUME /home/hexo/blog
WORKDIR /home/hexo/blog
RUN npm install -g hexo-cli
RUN hexo init /home/hexo/blog && cd /home/hexo/blog && npm install
EXPOSE 8080
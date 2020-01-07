FROM node:8.15.0-alpine

#add git >>
RUN apk --update add git less openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/* && \
#<< add git

#mod timezone>>
    apk add -U tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
#<<mod timezone

#set npm registry >>
    npm config set registry https://registry.npm.taobao.org && \
#<<set npm registry

#install gulp>>
    npm install -g gulp && \
#<<install gulp

#install yarn
    npm install -g yarn && \
    yarn config set registry https://registry.npm.taobao.org && \
#<<install yarn

#install pm2
    yarn global add pm2
#<<install pm2

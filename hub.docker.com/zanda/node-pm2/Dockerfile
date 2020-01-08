FROM node:10.16.0

# Change TimeZone
RUN apt-get install -y tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone

ENV NODE_PATH=/usr/local/lib/node_modules:$PATH

# Install PM2 && Other Package
RUN npm install pm2 yarn http-server cnpm express connect-history-api-fallback -g

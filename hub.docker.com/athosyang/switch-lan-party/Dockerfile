FROM node:8-alpine

#RUN npm config set registry http://registry.npm.taobao.org/ 

RUN wget https://github.com/spacemeowx2/switch-lan-play/archive/master.zip -O /tmp/slp.zip; \
    cd /tmp ; unzip /tmp/slp.zip ; \
    cp -r switch-lan-play-master/server /app ; \
    rm -rf /tmp/* ; \
    cd /app ; \
    npm install ; \
    npm run build ; \
    rm -rf node_modules ; \
    npm install --save-prod ; \
    rm -rf /root/.npm* 
    
WORKDIR /app

CMD [ "npm", "run", "server" ]
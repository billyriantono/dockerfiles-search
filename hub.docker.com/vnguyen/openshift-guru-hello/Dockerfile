FROM vnguyen/openshift-guru-base:centos7-nodejs

COPY app.js package.json $APP_HOME
RUN cd $APP_HOME \
    && npm install 

EXPOSE 3000

CMD ["npm", "start"]

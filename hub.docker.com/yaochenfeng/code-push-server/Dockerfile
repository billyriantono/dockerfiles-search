FROM node:alpine
COPY . /opt/codepush-server
WORKDIR /opt/codepush-server
RUN npm install
ENV COMMON_DATA_DIR /opt/codepush-server/data
ENV LOCAL_STORAGE_DIR /opt/codepush-server/storage
VOLUME [ "/tmp", "/opt/codepush-server/data", "/opt/codepush-server/storage" ]
EXPOSE 3000
CMD [ "./bin/www" ]
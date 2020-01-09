FROM readytalk/nodejs

WORKDIR /app
RUN npm install -g bootprint
RUN npm install -g bootprint-swagger
ENTRYPOINT ["/nodejs/bin/bootprint","swagger"]
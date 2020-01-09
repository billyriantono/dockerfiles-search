FROM node:latest

RUN mkdir parse

ADD . /parse
WORKDIR /parse
RUN npm install

# Optional (default : '/parse')
# ENV PARSE_MOUNT mountPath
ENV APP_ID setYourAppId
ENV DATABASE_URI setMongoDBURI
ENV MASTER_KEY setYourMasterKey
ENV CLIENT_KEY setYourClientKey

# Optional (default : 'parse/cloud/main.js')
# ENV CLOUD_CODE_MAIN cloudCodePath


EXPOSE 1337

# Uncomment if you want to access cloud code outside of your container
# A main.js file must be present, if not Parse will not start

VOLUME /parse/cloud               

CMD [ "npm", "start" ]

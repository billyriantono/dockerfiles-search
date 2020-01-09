FROM node:latest

RUN mkdir parse

ADD . /parse
WORKDIR /parse
RUN npm install

# Required
# ENV APP_ID app_id
# ENV MASTER_KEY master_key

# Optional (default : 'parse/cloud/main.js')
# ENV CLOUD_CODE_MAIN cloudCodePath

# Optional (default : '/parse')
# ENV PARSE_MOUNT mountPath

# EXPOSE 80

# Uncomment if you want to access cloud code outside of your container
# A main.js file must be present, if not Parse will not start
# VOLUME ./cloud /parse/cloud               

# CMD [ "npm", "start" ]

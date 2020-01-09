FROM keymetrics/pm2:latest-alpine


# Bundle APP files
COPY . /source 

ENV NPM_CONFIG_LOGLEVEL warn

WORKDIR /source
RUN npm install --production

# Show current folder structure in logs
# RUN ls -al -s

CMD [ "pm2-runtime", "start", "/source/pm2.json" ]
FROM keymetrics/pm2:latest-jessie

# Bundle APP files
WORKDIR /app
ADD . /app

# Install app dependencies
ENV NPM_CONFIG_LOGLEVEL warn
RUN npm install --production

# Show current folder structure in logs
RUN ls -al -R

CMD [ "pm2-runtime", "start", "pm2.json" ]
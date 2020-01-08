FROM node:9.11.2
# Create app directory
ENV APP_WORKDIR=/usr/src/app
WORKDIR $APP_WORKDIR

RUN npm i -g npm@4.6.1

# Copy dependency
ADD package.json $APP_WORKDIR
RUN yarn install --pref-offline

# Bundle app source!
COPY . .

# Run Application
CMD ["npm", "start"]

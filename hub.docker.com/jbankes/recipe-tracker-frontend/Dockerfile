FROM node:12.13-alpine3.9

# Work in app dir
WORKDIR app

# install dependencies; goal: leverage layering for quicker builds
COPY package*.json ./
RUN npm install

# Copy over files; be specific to minimize potentially including incorrect file
COPY src/ src/
COPY angular.json angular.json
COPY browserslist browserslist
COPY tsconfig.app.json tsconfig.app.json
COPY tsconfig.json tsconfig.json
COPY tslint.json tslint.json

EXPOSE 4200/tcp

ENTRYPOINT ["npm", "run", "ng", "serve", "--", "--host", "0.0.0.0"]

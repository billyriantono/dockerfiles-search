FROM node as angularBuild
WORKDIR /angular
## RUN npm install -g @angular/cli
ENV NODE_ENV=dev
COPY ["package.json", "package-lock.json*","./angular.json", "tsconfig.json", "./"]
COPY ["./src", "./src"]
RUN npm install
RUN npm run build:prod

FROM node
ENV PORT=1010
ENV ISSUER_WELLKNOWN=https://api.preprod.fusionfabric.cloud/login/v1/sandbox/.well-known/openid-configuration
ENV CLIENT_ID_B2C=yyyyy-yyyy-yyyy-yyyy-xxxxxxxx
ENV CLIENT_SECRET_B2C=yyyyyyy-yyyy-yyyy-yyyy-xxxxxxxx
ENV CALL_BACK_URI_B2C=http://localhost:1010/auth/cb/b2c

ENV CLIENT_ID_B2E=xxxxxxxxx-xxxxx-xxxx-yyyy-xxxxxxx
ENV CLIENT_SECRET_B2E=yyyyyyy-yyyyy-yyyyy-yyyy-xxxxxxx
ENV CALL_BACK_URI_B2E=http://localhost:1010/auth/cb/b2e

ENV CLIENT_ID_B2B=xxxxxx-xxxxxxxx-xxxxxxxx
ENV CLIENT_SECRET_B2B=yyyyyyyy-yyyyy-yyyy-yyyyy-xxxxxx

ENV SESSION_SECRET="SOME STRONG SECRET STRING"

ENV API_RESOURCE=https://dh-serviceprovider-api.azurewebsites.net/
ENV API_RESOURCE_TIMEOUT=5000

WORKDIR /app
COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --production --silent
COPY ./index.js .
COPY ./server ./server
COPY --from=angularBuild /angular/dist ./dist
EXPOSE 80
CMD npm start
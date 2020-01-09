FROM node:10-alpine AS auth-build

# Create app directory
WORKDIR /auth-server
COPY ./auth-server/package*.json ./
RUN npm install
COPY ./auth-server .
RUN npm run tsc
#at this point we have our /build folder with app and all dependencies
#---------------------------------------------------------------------------------

FROM node:10-alpine AS login-build

WORKDIR /login
COPY ./login .
RUN npm install 
RUN npm run build-prod
#--------------------------------------------------------------------------------

FROM node:12-alpine AS Release
WORKDIR /auth-server

COPY ./auth-server/package*.json ./

RUN npm install --prod
COPY --from=auth-build ./auth-server/build ./app
COPY --from=auth-build ./auth-server/keys ./keys
COPY --from=login-build ./login/dist/login ./login

EXPOSE 8080
CMD node ./app/auth.js

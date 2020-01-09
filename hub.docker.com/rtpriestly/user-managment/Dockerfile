FROM node:10.16-alpine AS api-build

# Create app directory
WORKDIR /api
COPY ./Api/package*.json ./
RUN npm install
COPY ./Api .
RUN npm run tsc
#at this point we have our /build folder with app and all dependencies
#---------------------------------------------------------------------------------

FROM node:10.16-alpine AS frontend-build

WORKDIR /Frontend
COPY ./Frontend .
RUN npm install 
RUN npm run build-prod && ls
#--------------------------------------------------------------------------------

FROM node:10.16-alpine AS Release
WORKDIR /app

COPY ./Api/package*.json ./

RUN npm install --prod
COPY --from=api-build ./api/build ./server
COPY --from=frontend-build ./Frontend/dist/Frontend ./Frontend
RUN cd ./Frontend && ls
EXPOSE 4040
CMD node ./server/app.js

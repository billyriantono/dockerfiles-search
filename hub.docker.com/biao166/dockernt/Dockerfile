# https://nodejs.org/en/docs/guides/nodejs-docker-webapp/
FROM node:12-alpine as build-webapp
WORKDIR /app
#COPY server ./server
COPY webapp/package*.json ./
RUN npm install
# Add the rest of the CONTENTS of webapp to the WORKDIR
ADD webapp ./
RUN npm run build

FROM node:12-alpine as server
WORKDIR /app
COPY server/package*.json ./
RUN npm install --only=production
ADD server ./
COPY --from=build-webapp /app/dist /app/dist

# Set and expose the application port
ENV PORT="8080"
EXPOSE 8080

# There should only be one CMD call per docker container
CMD ["npm", "start"]

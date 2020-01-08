FROM mhart/alpine-node:12 as builder

WORKDIR /app
COPY . .

RUN ["npm", "install"]
RUN ["npm", "run", "build"]

EXPOSE 3000
ENTRYPOINT ["node", "__sapper__/build"]
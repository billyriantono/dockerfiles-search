FROM mhart/alpine-node:10 as back
ENV TZ="Europe/Amsterdam"
ENV NODE_ENV=production
WORKDIR /backend
COPY package*.json ./
RUN npm install --only=production
RUN npm install pm2@3.5.1 -g

# add node user & the node group
RUN addgroup -S node && adduser -S -G node node
RUN chown node:node -R /backend
# switch to the node:node as a security best practice
USER node

COPY . .

# Show current folder's contents in logs
RUN ls -al
EXPOSE 8080

CMD ["pm2-runtime", "start", "pm2.config.js", "start", "server.js", "--web", "9000"]
RUN echo "\e[104mAfter running the docker container the frontend will start at: http://localhost:8080\e[0m\n\n"

# docker build -t production_backend -f ./Dockerfile.prod .
# docker run -p 8080:8080 -d --name tg-backend -m "300M" --memory-swap "1G" production_backend

## https://github.com/keymetrics/docker-pm2
## https://pm2.keymetrics.io/docs/usage/deployment/
# docker exec -it tg-backend pm2 monit
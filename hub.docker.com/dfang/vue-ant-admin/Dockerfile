FROM node:11.10.0-stretch AS builder
RUN mkdir -p /app
WORKDIR /app
COPY package.json package.json
COPY yarn.lock yarn.lock
RUN yarn
ADD . .
RUN npm run build

# FROM node:11.10.1-alpine
# RUN npm install -g serve && mkdir -p /app
# WORKDIR /app
# RUN ls -al /app/
# COPY –-from=builder /app/dist/ ./
# # Step 9: Serve the app at port 8080 using the serve package
# CMD ["serve", "-s", ".", "-l", "8080"]

# # Step 9: Hot reloading
# # Comment line 28 and un-comment the next line to enable hot reloading:
# # CMD ["npm", "run", "serve"]

# # After un-commenting the file above, git push and execute the following command:
# # $ hasura microservice sync ui microservice/ui/app/src:/app/src
# # Open the microservice in a new tab and make some changes to files in src to see it live:
# # $ hasura microservice open ui

FROM abiosoft/caddy
RUN mkdir -p /app
WORKDIR /app
EXPOSE 2015
COPY --from=builder /app/dist/ ./
COPY Caddyfile /etc/Caddyfile
# CMD ["caddy", "-agree", $ACME_AGREE]
# CMD ["--conf", "/etc/Caddyfile", "--log", "stdout", "--agree=$ACME_AGREE"]
# https://hub.docker.com/r/abiosoft/caddy/dockerfile
# CMD ["--log", "stdout", "--agree=$ACME_AGREE"]
CMD ["--conf", "/etc/Caddyfile", "--agree=$ACME_AGREE"]




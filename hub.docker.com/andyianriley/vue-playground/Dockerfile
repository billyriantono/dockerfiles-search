FROM node:9.11 as build-deps
MAINTAINER Andy Riley <https://github.com/andyianriley>

COPY . /app
WORKDIR /app/
RUN cd /app && \
    yarn install && \
    yarn build

# Stage 2 - the production environment
FROM andyianriley/static-express-server:latest
COPY --from=build-deps /app/dist /server/static
EXPOSE 9080
CMD ["yarn", "start"]
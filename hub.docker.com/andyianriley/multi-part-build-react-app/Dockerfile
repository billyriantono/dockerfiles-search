# Stage 1 - the build process
FROM node:9.11 as build-deps
COPY . /app
WORKDIR /app/
RUN cd /app && \
    yarn install && \
    yarn build

# Stage 2 - the production environment
FROM andyianriley/static-express-server:latest
COPY --from=build-deps /app/build /server/static
EXPOSE 8080
CMD ["yarn", "start"]

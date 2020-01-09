# Build stage
FROM node:lts-slim AS base
WORKDIR /app
COPY package.json .
RUN npm set progress=false && npm config set depth 0
RUN npm install --only=production
RUN cp -R node_modules prod_node_modules
RUN npm install

# Release stage
FROM base AS release
COPY --from=base /app/prod_node_modules /app/node_modules
COPY . /app
EXPOSE 3000
CMD ["npm","start"]
# Build
FROM node:10 as build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Run
FROM node:10
WORKDIR /app
COPY --from=build /app/package*.json /app/
COPY --from=build /app/dist /app/dist
COPY --from=build /app/config /app/config
RUN npm ci --only=prod
EXPOSE 8080
ARG BUILD=undetermined
ENV BUILD=$BUILD
CMD ["npm", "run", "start"]

FROM node:10 AS backend-build
RUN git clone https://github.com/dcsfuerth/docker-workshop-zitate.git
WORKDIR /docker-workshop-zitate/backend
RUN npm install --silent && npm run build

FROM node:10-alpine AS backend-server
COPY --from=backend-build /docker-workshop-zitate/backend/dist/ /app/
COPY --from=backend-build /docker-workshop-zitate/backend/package.json /app/
COPY --from=backend-build /docker-workshop-zitate/backend/data /data
WORKDIR /app
RUN npm install --only=prod
CMD ["node", "main.js"]

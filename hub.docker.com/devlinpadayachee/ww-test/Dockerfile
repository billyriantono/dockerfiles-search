FROM node:10
COPY ./ /app
WORKDIR /app
RUN npm install && npm run build-test

ENV NODE_ENV=test

FROM nginx
RUN mkdir /app
COPY --from=0 /app/dist /app
COPY nginx.conf /etc/nginx/nginx.conf

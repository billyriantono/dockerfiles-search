# STAGE - BUILD
FROM node:8 as build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . ./
RUN npm run build

# STAGE - DEPLOY
FROM nginx:1.14 as deploy
RUN rm -rf /usr/share/nginx/html/*
COPY --from=build /app/dist/* /usr/share/nginx/html/
COPY nginx-custom.conf /etc/nginx/conf.d/default.conf

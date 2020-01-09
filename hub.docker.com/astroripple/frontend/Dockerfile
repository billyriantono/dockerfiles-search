# ビルド環境
FROM node:alpine as build-stage
WORKDIR /app
COPY vue-project ./
RUN apk update && \
    npm install -g npm && \
    npm install -g @vue/cli && \
    npm install  && \
    npm run build

# 本番環境
FROM nginx:alpine as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
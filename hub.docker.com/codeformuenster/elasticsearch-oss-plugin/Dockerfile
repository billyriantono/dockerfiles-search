# Build
FROM node:carbon as builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
EXPOSE 8080
ARG BRANCH=master
ENV VUE_APP_BRANCH=$BRANCH
ARG BUILD=local
ENV VUE_APP_BUILD=$BUILD
RUN npm run build

# Run
FROM nginx:stable-alpine
COPY nginx.conf /etc/nginx/conf.d/ui.conf
COPY --from=builder /app/dist ./serve
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
EXPOSE 8080
CMD ["nginx"]

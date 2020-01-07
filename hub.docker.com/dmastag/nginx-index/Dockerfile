FROM nginx:stable-alpine

# Setup Timezone
RUN apk add --update tzdata
ENV TZ=Asia/Jakarta

RUN mkdir /http
COPY nginx.conf /etc/nginx/nginx.conf

#当使用nginx镜像，就要上传dist文件夹
FROM nginx
MAINTAINER keling <841127052@qq.com>

COPY dist/ /usr/share/nginx/html


#使用node镜像

#FROM node:6.10.3-slim
#RUN apt-get update \    && apt-get install -y nginx
#WORKDIR /app
#COPY . /app/
#EXPOSE 80
#RUN  npm install \
#    && npm run build \
#    && cp -r dist/* /var/www/html \
#    && rm -rf /app
#CMD ["nginx","-g","daemon off;"]

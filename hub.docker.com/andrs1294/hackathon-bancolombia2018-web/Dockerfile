FROM node:8.9-alpine as builder
WORKDIR /opt/web
COPY . .
RUN npm install
RUN npm install -g stylus
WORKDIR /opt/web/app
RUN stylus style.styl -o style.css

FROM nginx:1.13.9-alpine  
WORKDIR /root/
COPY --from=builder /opt/web /usr/share/nginx/html
RUN  cd /usr/share/nginx/html && mkdir hackathon && mv app hackathon && mv node_modules hackathon && mv assets hackathon  
ADD nginx.conf /etc/nginx/nginx.conf
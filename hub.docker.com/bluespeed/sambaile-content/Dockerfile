FROM nginx:alpine

WORKDIR /usr/share/nginx/html

COPY . .

EXPOSE 80 443 	

CMD ["nginx", "-g", "daemon off;"]
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/
COPY css /usr/share/nginx/html/css
COPY images /usr/share/nginx/html/images

EXPOSE 80
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]

FROM nginx:1.11
MAINTAINER Schogini sree@schogini.com

COPY hello.html /usr/share/nginx/html/

CMD ["nginx", "-g", "daemon off;"]


# docker build -t webhw .
# docker run -d -p 8000:80 --name ngixserver webhw
# To Browse
# curl -s http://localhost:8000/hello.html

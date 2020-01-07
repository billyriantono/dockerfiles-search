FROM nginx:1.13.11

LABEL maintainer="Jason Raimondi <jason@raimondi.us>"

COPY nginx/include/ /etc/nginx/include
COPY nginx/nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /etc/letsencrypt/webrootauth

CMD ["nginx", "-g", "daemon off;"]

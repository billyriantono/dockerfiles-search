FROM docker.io/nginx:1.13.12-alpine
MAINTAINER 'ming'

# copy config
# copy nginx config
COPY conf/nginx.conf  /etc/nginx
# copy ming config
COPY conf/ming.conf  /etc/nginx/conf.d/default.conf

# copy ming  blog
COPY /hexo/public /usr/share/nginx/html

FROM nginx

#COPY default.conf /etc/nginx/conf.d/default.conf
COPY default.conf /etc/nginx/conf.d/default.template

EXPOSE 80
EXPOSE 443

#CMD /bin/bash -c "envsubst < /etc/nginx/conf.d/mysite.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"
CMD /bin/bash -c "envsubst < /etc/nginx/conf.d/default.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"

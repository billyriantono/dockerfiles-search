FROM nginx:alpine

# copy commonui static files
RUN mkdir -p /usr/share/nginx/html/commonui-bs3
COPY . /usr/share/nginx/html/commonui-bs3/

#COPY cors.conf /etc/nginx/conf.d/default.conf

# replace-string para corrigir domains (kubernetes)
#COPY ./scripts/* /opt/

# muda entrypoint, mantém cmd
#ENTRYPOINT ["/opt/ala-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]


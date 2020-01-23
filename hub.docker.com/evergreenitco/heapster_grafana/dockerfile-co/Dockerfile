FROM nginx:1.17

COPY web.key /etc/nginx/
COPY web.crt /etc/nginx/
COPY nginx-ssl-proxy.conf /etc/nginx/conf.d/

EXPOSE 443

CMD ["nginx", "-g", "daemon off;"]

#Imagen base
FROM nginx
#Copiar archivos
COPY build/es5-bundled /usr/share/nginx/html
COPY default.conf /etc/nginx/conf.d/default.conf
# puertos
EXPOSE 80
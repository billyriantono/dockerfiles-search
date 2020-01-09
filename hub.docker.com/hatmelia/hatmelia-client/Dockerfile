#
# --build-arg port=port_number
#
FROM nginx

#ARG server=http://localhost:3000/links-analyzer
#ENV HATMELIA_SERVER=$server

WORKDIR /usr/share/nginx/html

# Bundle app source
COPY dist ./dist
COPY index.html .

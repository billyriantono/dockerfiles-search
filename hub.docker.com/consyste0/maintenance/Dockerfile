FROM nginx:1.14-alpine
LABEL maintainer="contato@elementarsistemas.com.br"

# copia a configuração
COPY config/ /etc/nginx/

# copia o conteúdo html
COPY www/ /etc/nginx/html/

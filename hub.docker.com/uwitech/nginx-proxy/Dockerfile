FROM nginx:1.13-alpine

COPY nginx.conf /etc/nginx/nginx.conf
COPY utils/replace-vars /replace-vars
COPY cmd.sh /cmd.sh

CMD ./cmd.sh

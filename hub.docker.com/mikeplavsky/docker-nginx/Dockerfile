FROM nginx

RUN mkdir /etc/nginx/ssl && \ 
   openssl req -x509 \ 
   -nodes -days 365 \ 
   -newkey rsa:2048 \ 
   -subj "/C=UK/ST=MP/L=MP/O=MP/OU=MP/CN=mp.com" \ 
   -keyout /etc/nginx/ssl/server.key \ 
   -out /etc/nginx/ssl/server.crt

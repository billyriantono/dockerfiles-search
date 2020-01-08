FROM nginx

RUN apt update
RUN apt -y install net-tools curl dnsutils

ADD ./nginx.conf /etc/nginx/temp/nginx.conf
ADD docker_entrypoint.sh docker_entrypoint.sh

ENTRYPOINT ["./docker_entrypoint.sh"]

FROM nginx:1.13

LABEL AUTHOR="xwzhou@yeah.net"

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


RUN sed -i 's/worker_processes  1/worker_processes  auto/' /etc/nginx/nginx.conf

COPY conf.d/ /etc/nginx/conf.d/
COPY html/  /var/nginx/html/

WORKDIR  /var/nginx/html

CMD ["sh","-c","if [ -f '/var/nginx/html/index.html' ];then sed -i s/%NG_HOSTNAME%/$HOSTNAME/ /var/nginx/html/index.html; fi && nginx -g 'daemon off;'"]

EXPOSE 80

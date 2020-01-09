FROM busybox

LABEL git=https://github.com/ksaito1125/hello-docker
LABEL app=sample
ADD src/index,html /www/index.html
EXPOSE 8005
CMD httpd -p 8005 -h /www; tail -f /dev/null
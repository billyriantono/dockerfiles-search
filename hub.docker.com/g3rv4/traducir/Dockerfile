FROM microsoft/dotnet:2.1.6-aspnetcore-runtime-stretch-slim

RUN apt-get update && \
    apt-get install -y nginx supervisor && \
    apt-get clean

EXPOSE 80

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY app/ /var/app
COPY default-site /etc/nginx/sites-available/default

CMD ["/usr/bin/supervisord"]

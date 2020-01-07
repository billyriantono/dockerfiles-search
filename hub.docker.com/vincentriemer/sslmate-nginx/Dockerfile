FROM nginx:latest

# install prerequisites
RUN apt-get update
RUN apt-get -y install ca-certificates wget

# install sslmate
RUN wget -P /etc/apt/sources.list.d https://sslmate.com/apt/ubuntu1404/sslmate.list
RUN wget -P /etc/apt/trusted.gpg.d https://sslmate.com/apt/ubuntu1404/sslmate.gpg
RUN apt-get update
RUN apt-get -y install sslmate

# copy templates and scripts
COPY templates /templates
COPY template.sh /scripts/template.sh
COPY entrypoint.sh /scripts/entrypoint.sh

CMD ["bash", "/scripts/entrypoint.sh"]
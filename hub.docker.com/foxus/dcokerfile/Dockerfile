FROM ubuntu
RUN apt update -y
RUN apt upgrade -y
RUN apt install apache2 -y
EXPOSE 8080
CMD ["apache2ctl", "-D", "FOREGROUND"]

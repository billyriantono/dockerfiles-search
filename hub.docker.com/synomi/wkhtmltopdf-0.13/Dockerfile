FROM debian:jessie

MAINTAINER Kai Heikka <synomi66@gmail.com>
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install apt-utils libpng12-0 libjpeg62-turbo libssl1.0.0 libfreetype6 libicu52 fontconfig libx11-6 libxext6 libxrender1 libxcb1 xfonts-base xfonts-75dpi xvfb -y

ADD wkhtmltox-0.13.0-alpha-7b36694_linux-jessie-amd64.deb /root/
RUN dpkg -i /root/wkhtmltox-0.13.0-alpha-7b36694_linux-jessie-amd64.deb

RUN apt-get clean
RUN apt-get autoclean

# Add startup script
ADD startup /usr/bin/startup
RUN chmod 755 /usr/bin/startup

# Execute startup script to keep container running
CMD [ "/usr/bin/startup" ]

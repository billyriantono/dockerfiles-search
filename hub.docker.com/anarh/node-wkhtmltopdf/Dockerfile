FROM node:0.10.38
MAINTAINER Emmanuel (Manny) Narh <eanarh@gmail.com>

RUN cd /tmp \
	&& apt-get update \
	&& apt-get install -y \
		xfonts-base \
		xfonts-75dpi \
		xserver-common \
	&& curl -SLO "http://downloads.sourceforge.net/project/wkhtmltopdf/0.12.2.1/wkhtmltox-0.12.2.1_linux-jessie-amd64.deb" \
	&& dpkg -i wkhtmltox-0.12.2.1_linux-jessie-amd64.deb 

CMD ["node"]
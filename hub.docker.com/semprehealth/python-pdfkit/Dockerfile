FROM semprehealth/python:1.0
MAINTAINER Joshua Primas "josh@semprehealth.com"

RUN apt-get update && apt-get upgrade -y
RUN apt-get install xfonts-75dpi xfonts-base -y
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb
RUN dpkg -i wkhtmltox_0.12.5-1.stretch_amd64.deb

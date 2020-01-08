FROM circleci/python:3.6.9-stretch

ENV WKHTMLTOPDF_VERSION 0.12.3

USER root

RUN apt-get update && apt-get --no-install-recommends install -y locales-all gettext

RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/$WKHTMLTOPDF_VERSION/wkhtmltox-${WKHTMLTOPDF_VERSION}_linux-generic-amd64.tar.xz \
    && tar -xJf wkhtmltox-*.tar.xz \
    && rm -f wkhtmltox/bin/wkhtmltoimage \
    && cp -R wkhtmltox/* /usr \
    && rm -Rf wkhtmltox*

USER circleci
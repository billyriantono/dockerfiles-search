FROM node:6

# install wkhtmltopdf
RUN mkdir -p ~/wkhtmltopdf \
    && curl -SL http://download.gna.org/wkhtmltopdf/0.12/0.12.3/wkhtmltox-0.12.3_linux-generic-amd64.tar.xz \
    | tar -xJC ~/wkhtmltopdf \
    && mv ~/wkhtmltopdf/wkhtmltox/bin/wkhtmltopdf /usr/local/bin/wkhtmltopdf \
    && chmod +x /usr/local/bin/wkhtmltopdf \
    && rm -r ~/wkhtmltopdf

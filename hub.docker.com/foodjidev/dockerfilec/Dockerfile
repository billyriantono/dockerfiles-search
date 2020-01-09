FROM golang

RUN apt-get clean && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
    gdebi \
    wget \
    xvfb
RUN wget https://downloads.wkhtmltopdf.org/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-jessie-amd64.deb
RUN gdebi --n wkhtmltox-0.12.2.1_linux-jessie-amd64.deb
RUN rm wkhtmltox-0.12.2.1_linux-jessie-amd64.deb
RUN echo '#!/bin/bash\nxvfb-run -a --server-args="-screen 0, 640x480x16" /usr/local/bin/wkhtmltopdf -q $*' > /usr/local/bin/wkhtmltopdf.sh
RUN chmod a+x /usr/local/bin/wkhtmltopdf.sh
RUN ln -s /usr/local/bin/wkhtmltopdf.sh /usr/local/bin/wkhtmltopdf-with-xvfb

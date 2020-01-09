FROM openjdk:8-jre

#RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
COPY wkhtmltox-0.12.4_linux-generic-amd64.tar.xz /home/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
RUN tar -xvf /home/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
RUN mv wkhtmltox/bin/wkhtmltopdf /usr/local/bin && chmod a+x /usr/local/bin/wkhtmltopdf
RUN rm -f /usr/wkht
ADD simsun.ttc /usr/share/fonts/simsun.ttc
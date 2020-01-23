FROM python:3

RUN apt-get update
RUN pip3 install pipenv
RUN apt-get install -y nginx
RUN systemctl enable nginx
RUN apt-get install -y git
RUN apt-get install -y vim

EXPOSE 80
EXPOSE 8080

RUN git clone https://github.com/bennyro/webenny1.0.git /app/

WORKDIR /app/

RUN chmod +x start_webuddha.sh
RUN chmod +x websockets_runner.py

RUN cp public-html/index.html /var/www/html/
RUN cp start_webuddha.sh /usr/local/bin/
RUN ln -s usr/local/bin/start_webuddha.sh /

RUN pipenv install --system

ENTRYPOINT ["start_webuddha.sh"]

FROM debian

RUN apt-get update \
&& apt-get install -y \
    uwsgi \
    uwsgi-plugin-python3 \
    unoconv \
    python3-pip \
&& apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD ./ /
RUN chmod +x /startup.sh
RUN pip3 install -r /app/requirements.txt

EXPOSE 8000

WORKDIR /app
VOLUME /templates

CMD ["/startup.sh"]

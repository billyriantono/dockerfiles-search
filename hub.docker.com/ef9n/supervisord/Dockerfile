FROM python:3.7.1

LABEL maintainer="Fatih Sarhan <f9n@protonmail.com>"
LABEL version="0.1.0"

WORKDIR /etc/supervisor

RUN pip install git+https://github.com/Supervisor/supervisor \
  && echo_supervisord_conf > /etc/supervisor/supervisord.conf \
  && sed -i 's/^\;\(\[inet_http_server\]\)/\1/' supervisord.conf \
  && sed -i 's/^\;\(port=\)127.0.0.1/\1 */' supervisord.conf 

EXPOSE 9001

ENTRYPOINT ["/usr/local/bin/supervisord"]
CMD ["-n"]

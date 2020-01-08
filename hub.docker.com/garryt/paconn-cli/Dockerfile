FROM python:3.5

VOLUME /usr/app/paconn
WORKDIR /usr/app/paconn

RUN useradd --create-home --shell /bin/bash paconn && \
    usermod -aG sudo paconn && \
    chown -R paconn:paconn /usr/app/paconn

RUN pip install paconn>=0.0.10

CMD /bin/bash
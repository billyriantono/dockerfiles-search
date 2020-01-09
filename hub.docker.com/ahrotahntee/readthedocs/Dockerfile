FROM alpine:latest
WORKDIR /srv
ENV PATH $PATH:/venv/bin
RUN apk update && apk add git py3-pip python3 py3-virtualenv alpine-sdk py3-lxml py3-lxml py3-libxml2 zlib-dev libxslt-dev libxml2-dev py3-libxml2 gcc python3-dev
RUN git clone https://github.com/rtfd/readthedocs.org.git
RUN cd readthedocs.org
RUN virtualenv /venv
RUN pip install -r /srv/readthedocs.org/requirements.txt
WORKDIR /srv/readthedocs.org
RUN python manage.py migrate
RUN python manage.py collectstatic
ENTRYPOINT ["/venv/bin/python", "manage.py", "runserver"]

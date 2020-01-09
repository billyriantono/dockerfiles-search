FROM alpine:3.10.1

RUN echo "**** apk update ****" && \
    apk update

RUN echo "**** install Python ****" && \
    apk add --no-cache python3 && \
    if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi && \
    \
    echo "**** install pip ****" && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache --upgrade pip setuptools wheel && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi

RUN echo "**** apk install sqlite ****" && \
    apk add --no-cache sqlite

RUN echo "**** pip install sqlite3 ****" && \
    pip3 install --no-cache pysqlite3

RUN echo "**** install requests ****" && \
    pip3 install --no-cache requests

RUN echo "**** install flask ****" && \
    pip3 install --no-cache flask

RUN echo "**** install sentry-sdk ****" && \
    pip3 install --no-cache sentry-sdk==0.10.2

ADD server.py /

ADD templates $HOME/templates

ADD testdb $HOME/db/testdb

ENV FLASK_APP="server.py"

CMD ["flask", "run", "--host=0.0.0.0", "--port=80"]

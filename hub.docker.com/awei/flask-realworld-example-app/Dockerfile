FROM awei/flask-devenv

ENV FLASK_APP=autoapp.py
ENV FLASK_DEBUG=1

RUN git clone https://github.com/chenwei791129/flask-realworld-example-app.git

WORKDIR /flask-realworld-example-app

RUN pip install -r requirements/dev.txt && \
    export CONDUIT_SECRET=$(cat /proc/sys/kernel/random/uuid) && \
    flask db init && \
    flask db migrate && \
    flask db upgrade

EXPOSE 5000/tcp

ENTRYPOINT [ "flask" ]

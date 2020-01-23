FROM python:3

WORKDIR /app

COPY requirements-src.txt /app/

RUN pip install -r /app/requirements-src.txt && rm -rf /tmp/* /root/.cache

COPY . /app

RUN python -m compileall . && rm -rf /tmp/* /root/.cache

#ENTRYPOINT  [ "/app/entrypoint.sh" ]
#CMD []

USER nobody



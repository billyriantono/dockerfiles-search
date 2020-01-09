
FROM simsemand/chronos
MAINTAINER PmoshBR

RUN pip install --upgrade pip
RUN pip install cython
RUN apk add --no-cache freetds-dev
RUN pip install pymssql

EXPOSE 5000
VOLUME /chronos
ENV CHRONOS_PATH=/chronos
ENV CHRONOS=yes_sir_docker

WORKDIR /app/chronos
ENTRYPOINT python chronos.py

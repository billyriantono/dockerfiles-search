#FROM python:3.7-slim-buster
FROM tiangolo/uwsgi-nginx-flask:python3.7


RUN apt-get update && apt-get install -y \
    libaio1 libaio-dev \
 && rm -rf /var/lib/apt/lists/*
 
COPY ./requirements.txt /app/requirements.txt
WORKDIR /app
RUN pip install -r requirements.txt


#setup oracle paths
ENV ORACLE_HOME=/usr/lib/oracle/18.1/client64
ENV LD_LIBRARY_PATH=$ORACLE_HOME/lib
ENV PATH=$ORACLE_HOME/bin:$PATH


COPY . /app

RUN cd pyLib && python setup.py build install && \
	cd ../my-dash-core-components && pip install . && \
	cd .. && rm -rf pyLib my-dash-core-components && \
	mv defaults.cfg ../  && \
	mv setup.sh / && chmod 700 /setup.sh && \
	mkdir -p /usr/lib/oracle/18.1/client64/ && \
	unzip /app/oracle.zip -d /usr/lib/oracle/18.1/client64/ && \
	ln -s /usr/lib/oracle/18.1/client64/lib/libclntsh.so.18.1 /usr/lib/oracle/18.1/client64/lib/libclntsh.so && \
	ln -s /usr/lib/oracle/18.1/client64/lib/libocci.so.18.1 /usr/lib/oracle/18.1/client64/lib/libocci.so && \
	pip install cx_Oracle --upgrade

EXPOSE 5000

ENTRYPOINT ["/setup.sh"]

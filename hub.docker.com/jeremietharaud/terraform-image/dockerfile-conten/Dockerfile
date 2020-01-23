FROM python:2.7

ENV HADDOP_EXPORTER_HOME /opt/hadoop_exporter

RUN apt-get update \
 && apt-get install python-pip python-dev python-setuptools git -y 

# Update Pip
RUN pip install --upgrade pip

WORKDIR ${HADDOP_EXPORTER_HOME}
ADD . ${HADDOP_EXPORTER_HOME}

RUN pip install -r requirements.txt

CMD python hadoop_exporter.py

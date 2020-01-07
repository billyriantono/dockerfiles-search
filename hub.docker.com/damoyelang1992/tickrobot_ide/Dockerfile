FROM python:2.7.13

RUN  mkdir /root/.pip
COPY ./pip.conf    /root/.pip/pip.conf
COPY ./requirements.txt    /opt/requirements.txt
COPY  ./run.sh    /run.sh

RUN  chmod 755 /run.sh
RUN pip install -r /opt/requirements.txt

VOLUME ["/opt/code"]

EXPOSE 5000

#CMD ["python", "/opt/code/run.py"]
CMD  /run.sh

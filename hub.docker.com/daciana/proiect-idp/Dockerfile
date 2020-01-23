FROM python:3
USER root
WORKDIR /

RUN pip3 install mysql-connector
ADD worker2.py /
CMD [ "python3", "./worker2.py" ]



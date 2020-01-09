FROM terragontech/python

MAINTAINER Terragon DCB Team <tech@terragonltd.com>

RUN cd /

RUN mkdir production

WORKDIR /production
ADD service_microservice/libraries  /production/libraries

ADD logs /production/logs

ADD service_microservice/service.py /production/service.py

ADD service_microservice/requirements.txt /production/requirements.txt

RUN pip install -r requirements.txt

EXPOSE 8081

CMD python service.py



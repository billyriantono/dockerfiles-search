FROM python:3

WORKDIR /opt/

RUN pip install flask requests web3 wasp-eureka python-jose

COPY * /opt/

EXPOSE 10000

CMD python runAll.py $V1 $V2 $V3 $V4;



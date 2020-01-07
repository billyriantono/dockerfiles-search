FROM python:3.7-alpine

RUN pip install --upgrade pip

RUN mkdir -p /opt/microservices
ADD scripts/base_distributor.py /opt/microservices
ADD scripts/common.py /opt/microservices
ADD scripts/jenkins_stats.py /opt/microservices
ADD scripts/producer_test.py /opt/microservices
ADD scripts/consumer_test.py /opt/microservices
ADD scripts/message_parser.py /opt/microservices
ADD scripts/log_processor.py /opt/microservices
RUN chmod +x /opt/microservices/*

RUN pip3 install flask flask_cors python-dateutil kafka-python pymongo parse supervisor
ADD supervisor.conf /etc/supervisord.conf

CMD ["supervisord", "-n"]
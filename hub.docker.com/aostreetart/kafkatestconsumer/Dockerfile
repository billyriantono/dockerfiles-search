FROM python:3

RUN pip install kafka-python

ADD KafkaDockerConsumer.py .

ENTRYPOINT ["python", "KafkaDockerConsumer.py"]

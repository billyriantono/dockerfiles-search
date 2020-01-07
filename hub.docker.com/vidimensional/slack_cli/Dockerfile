FROM python:3.6-alpine

COPY requirements.txt /opt/requirements.txt

RUN pip install -r /opt/requirements.txt

COPY src/slack.py /opt/slack.py

ENTRYPOINT [ "/opt/slack.py" ]

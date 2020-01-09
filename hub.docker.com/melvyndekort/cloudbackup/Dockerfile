FROM python:3.7.0-alpine3.8

RUN pip install --upgrade --no-cache-dir pip
RUN pip install --no-cache-dir b2 awscli schedule

COPY job.py /

CMD ["python", "-u", "/job.py"]

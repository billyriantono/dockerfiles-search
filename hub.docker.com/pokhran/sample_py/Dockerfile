FROM python:3.7.1-alpine3.8

WORKDIR /workspace

COPY tester.py /workspace/tester.py

RUN pip install boto3

CMD [ "/bin/sh", "-c", "python /workspace/tester.py"]

FROM python:3.7-alpine

ADD . /

RUN  pip install -r requirements.txt
EXPOSE 9090

CMD ["python", "/app.py"]

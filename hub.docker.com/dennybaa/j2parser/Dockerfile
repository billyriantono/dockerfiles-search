FROM python:2.7-alpine3.8

ADD . /code

RUN cd /code && pip install -r requirements.txt && \
    sed -i 's/host=config.HOST/host="0.0.0.0"/g' parser.py

EXPOSE 5000
CMD ["python", "/code/parser.py"]

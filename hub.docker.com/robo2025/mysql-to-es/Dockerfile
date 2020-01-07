FROM robo2025/python:3.6-alpine
ENV PYTHONUNBUFFERED 1


COPY . /project/mysql_to_es

WORKDIR /project/mysql_to_es

RUN pip install -r requirements.txt \
    && mkdir -p /project/mysql_to_es/logs

RUN apk --no-cache add tzdata  && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone

CMD python sync_mysql_to_es.py
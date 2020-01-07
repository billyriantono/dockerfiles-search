FROM python:3.5.7-stretch

RUN apt-get update \
    && pip3 install pandas==0.24 \
    && pip3 install pymongo \
    && pip3 install sqlalchemy \
    && pip3 install psycopg2

WORKDIR /home/ubuntu/incentives

CMD ["python3 Heropayroll_Daily.py"]

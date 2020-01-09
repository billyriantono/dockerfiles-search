FROM python:2.7-alpine3.7
RUN apk add --no-cache ca-certificates
RUN apk add --no-cache gcc g++ bash

RUN pip install flask wget
RUN pip install py4j pandas cassandra-driver
RUN pip install requests pypinyin ConfigParser arrow regex

COPY . /app
WORKDIR /app

CMD ["python", "main.py"]

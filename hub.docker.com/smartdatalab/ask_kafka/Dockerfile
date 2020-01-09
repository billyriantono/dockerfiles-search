FROM python:3.7-alpine
RUN apk add --no-cache gcc libc-dev unixodbc-dev
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY /ask_kafka_rest /ask_kafka_rest
WORKDIR /ask_kafka_rest
CMD ["gunicorn", "-b", "0.0.0.0:8085", "--workers", "8", "--timeout", "300", "ask_kafka_rest:app"]

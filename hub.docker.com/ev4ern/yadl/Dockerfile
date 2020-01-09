FROM python:3.7-alpine

WORKDIR /app

CMD ["python", "main.py"]

RUN apk add --no-cache python-dev openssl-dev libffi-dev musl-dev gcc

ADD requirements.txt .

RUN pip install -r requirements.txt

ADD app .

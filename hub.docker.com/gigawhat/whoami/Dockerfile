FROM python:3.6.5-alpine3.7

ADD app.py requirements.txt /app/

ENV PORT 5000

RUN adduser -D app

WORKDIR /app

RUN pip install -r requirements.txt

USER app

CMD ["python", "app.py"]

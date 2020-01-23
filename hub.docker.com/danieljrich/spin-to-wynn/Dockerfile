FROM python:3.6-slim-jessie

ENV PYTHONUNBUFFERED=1

WORKDIR /app/
COPY function/. .
COPY requirements.txt .
RUN pip3 install -r requirements.txt

ENTRYPOINT ["python3", "main.py"]

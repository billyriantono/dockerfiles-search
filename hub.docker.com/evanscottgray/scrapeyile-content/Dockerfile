FROM python:3.7-alpine

WORKDIR /app

CMD ["python", "main.py"]

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY main.py .

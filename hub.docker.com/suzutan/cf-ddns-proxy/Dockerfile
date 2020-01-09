FROM python:3-alpine

WORKDIR /app

ADD requirements.txt .
RUN pip install -r requirements.txt
ADD app.py .


ENTRYPOINT ["python", "app.py"]
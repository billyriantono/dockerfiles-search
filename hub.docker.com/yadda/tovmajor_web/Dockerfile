FROM python:3-slim

EXPOSE 80

WORKDIR /code

ADD /app /code

RUN pip install -r requirements.txt



CMD ["python", "./main.py"]
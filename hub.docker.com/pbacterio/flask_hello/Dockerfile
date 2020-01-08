FROM python:alpine

ENV FLASK_APP hello_app.py
EXPOSE 5000/tcp

WORKDIR /app
COPY . .
RUN pip install -r requirements.txt

ENTRYPOINT flask run --host=0.0.0.0
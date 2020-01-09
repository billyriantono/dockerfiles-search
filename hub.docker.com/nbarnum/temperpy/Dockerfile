FROM python:3.7-alpine
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
ENTRYPOINT ["/usr/local/bin/python", "/app/temper.py"]

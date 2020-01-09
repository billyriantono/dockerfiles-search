FROM python:3.7
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
ENTRYPOINT ["/usr/local/bin/python","app.py"]
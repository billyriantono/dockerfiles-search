FROM python:latest
RUN mkdir -p /app
RUN mkdir -p /config
COPY . /app
RUN pip install /app
CMD [ "python", "/app/main.py" ]

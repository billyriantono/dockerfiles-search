FROM tiangolo/uwsgi-nginx-flask:python3.6
RUN apt-get update -y \ 
    && apt-get install -y libgtk2.0-dev \
    && apt-get install -y tesseract-ocr \
    && rm -rf /var/lib/apt/lists/*

ENV LISTEN_PORT=5000
EXPOSE 5000

COPY ./app /app
RUN pip install -r ./requirements.txt --no-cache-dir


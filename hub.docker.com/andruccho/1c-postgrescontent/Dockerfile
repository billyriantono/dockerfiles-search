FROM pypy:3.6-7-slim

LABEL maintainer="Andrij David <david@geek.mg>"

COPY ./start.sh /start.sh
RUN chmod +x /start.sh

COPY ./gunicorn_conf.py /gunicorn_conf.py

COPY ./start-reload.sh /start-reload.sh
RUN chmod +x /start-reload.sh

COPY ./app /app
WORKDIR /app/

RUN apt update && apt -y upgrade && apt install -y build-essential

RUN pypy3 -m ensurepip

RUN pip install --no-cache-dir uvicorn gunicorn

RUN rm -rf /var/lib/apt/lists/*

ENV PYTHONPATH=/app

EXPOSE 80

# Run the start script, it will check for an /app/prestart.sh script (e.g. for migrations)
# And then will start Gunicorn with Uvicorn
CMD ["/start.sh"]

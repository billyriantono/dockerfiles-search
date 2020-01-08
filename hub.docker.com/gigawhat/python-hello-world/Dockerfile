FROM python:3.6.5-alpine3.7
ADD app.py requirements.txt /app/
RUN adduser -D app
WORKDIR /app
RUN pip install -q -r requirements.txt
USER app
ENV PORT 8000
ENV GUNICORN_CMD_ARGS "--access-logfile -"
EXPOSE 8000
CMD gunicorn -b 0.0.0.0:${PORT} app:app

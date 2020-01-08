FROM python:3.6.8-slim-stretch
#FROM python:2.7.16-slim-stretch

COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENV FLASK_APP core.py
ENV PARAMETER=MY_PARAMETER

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT [ "docker-entrypoint.sh" ]

EXPOSE 5000

CMD [ "python", "-m", "flask", "run", "--host=0.0.0.0" ]
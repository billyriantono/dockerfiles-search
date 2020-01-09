FROM python:2

COPY ./web /app/web
COPY requirements.txt /app

# uh, root required for some python packages - not ideal!
WORKDIR /app
RUN pip install -r requirements.txt

RUN chmod 777 ./web/wait-for-influxdb.sh
RUN useradd -ms /bin/bash admin
USER admin

EXPOSE 5000
ENV FLASK_APP web/index.py
CMD ["./web/wait-for-influxdb.sh", "influxdb", "flask", "run", "--host=0.0.0.0"]

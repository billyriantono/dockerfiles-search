FROM python:2.7

RUN export FLASK_APP=app.py
COPY requirements.txt /app/
RUN pip install -r /app/requirements.txt
COPY . /app/

WORKDIR ./app

CMD ["flask", "run"]

FROM tiangolo/uwsgi-nginx-flask:python3.6

#COPY requirements.txt /tmp/requirements.txt

#RUN pip install --no-cache-dir -r /tmp/requirements.txt

COPY . /app

RUN pip install /app

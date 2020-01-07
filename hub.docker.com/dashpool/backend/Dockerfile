FROM tiangolo/uwsgi-nginx-flask:python3.7

COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
EXPOSE 5000
FROM tiangolo/uwsgi-nginx-flask:python3.6


COPY ./app/requirements.txt  requirements.txt

# upgrade pip and install required python packages
RUN pip install -U pip
RUN pip install -r requirements.txt

COPY ./app /app

FROM python:3.7-alpine
COPY requirements.txt /
RUN pip install -r /requirements.txt
COPY flaskr /projects/flaskblog/flaskr
WORKDIR /projects/flaskblog
EXPOSE 5000
CMD flask run --port 5000

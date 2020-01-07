FROM python:3.6-alpine
RUN mkdir -p /opt/flask/src
COPY requirements.txt /opt/flask/src/
WORKDIR /opt/flask/src
RUN pip install -r requirements.txt
COPY app.py /opt/flask/src
EXPOSE 5000
CMD python app.py

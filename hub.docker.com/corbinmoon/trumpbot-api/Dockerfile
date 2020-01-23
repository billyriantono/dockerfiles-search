FROM python:3

MAINTAINER  "clangmoon@gmail.com"

RUN pip install tensorflow && pip install textgenrnn && pip install flask && pip install flask-restful && pip install -U flask-cors
RUN git clone --branch master https://github.com/CorbinMoon/trumpBoT-api
RUN cd /trumpBoT-api

WORKDIR  /trumpBoT-api

COPY .  /trumpBoT-api

ENV FLASK_APP api.py

# flask default port
EXPOSE 5000

CMD ["flask", "run", "--host", "0.0.0.0"]


FROM python:3
MAINTAINER marquirj



RUN apt-get install -y git
COPY . .
RUN pip install -r requirements.txt
EXPOSE 80
CMD  cd bot && python app.py

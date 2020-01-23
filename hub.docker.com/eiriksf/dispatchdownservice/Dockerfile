#FROM python:3.7.0
#COPY src /app
#COPY requirements.txt /app
#WORKDIR /app
#RUN pip install --upgrade pip
#RUN pip install -r requirements.txt
#WORKDIR /app
#EXPOSE 5000
#CMD gunicorn app:app --workers ${WORKERS:-8} --bind 0.0.0.0:5000 --access-logfile -

FROM python:3.7.0
COPY src /app
COPY requirements.txt /app
WORKDIR /app
RUN pip3 install pip==19.0.2
RUN pip3 install -r requirements.txt
WORKDIR /app
EXPOSE 5000
CMD [ "python", "app.py" ]


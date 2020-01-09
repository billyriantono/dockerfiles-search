FROM python:3.6
RUN apt update && apt upgrade -y
RUN	mkdir /data
WORKDIR /data
COPY requirements.txt /data
RUN pip install -r ./requirements.txt
COPY . /data
RUN python3 manage.py migrate
CMD ["python3","manage.py","runserver","0.0.0.0:8000"]
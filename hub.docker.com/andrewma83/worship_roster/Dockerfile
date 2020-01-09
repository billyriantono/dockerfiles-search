FROM python:3.5

WORKDIR /opt

RUN mkdir -p /opt/app
RUN mkdir -p /opt/data
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY app /opt/app

COPY flask_apps.py /opt/

COPY requirements.txt /opt/

RUN pip3 install -r /opt/requirements.txt

EXPOSE 5000

CMD ["python3", "/opt/flask_apps.py"]


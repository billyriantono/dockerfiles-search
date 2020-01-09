FROM centos
COPY requirements.txt requirements.txt
COPY web.py web.py
RUN yum install epel-release -y
RUN yum install python-pip -y
RUN yum install python-devel -y
RUN pip install --upgrade pip
#WORKDIR /root/python-flask
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]

CMD ["web.py"]

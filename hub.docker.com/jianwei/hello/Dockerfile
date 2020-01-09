FROM    centos
RUN     yum install wget -y
RUN     wget http://bottlepy.org/bottle.py
COPY    hello.py /hello.py
EXPOSE  8080
CMD     ["python","hello.py"]

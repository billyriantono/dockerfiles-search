FROM ubuntu

RUN apt-get update && apt-get -y upgrade \
	python \
	python-pip 

ADD test.py /tmp/ 
ADD run.sh /tmp/
RUN chmod u+x /tmp/run.sh

EXPOSE 5000

CMD /tmp/./run.sh

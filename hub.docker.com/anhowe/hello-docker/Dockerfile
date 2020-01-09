FROM ubuntu
MAINTAINER Anthony Howe <ahowe_ca@yahoo.ca>

RUN apt-get update && apt-get install -y \
	python 
	
COPY hellodocker /opt/start/.
		
WORKDIR /opt/start
		
CMD ["/usr/bin/python", "/opt/start/hellodocker.py"]

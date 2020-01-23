FROM debian

MAINTAINER Giannis Giannakopoulos


RUN apt-get update && apt-get install -y python python-pip sqlite3
ADD . /opt/buddy
RUN cd /opt/buddy && \
	pip install -r requirements.txt && \
	pip install . && \
	sed -i -e "/database/d" conf/buddy.yml  && \
	echo "database: \"/opt/buddy/database.db\"" >> conf/buddy.yml

ENTRYPOINT /opt/buddy/docker/entrypoint.sh /opt/buddy/conf/buddy.yml

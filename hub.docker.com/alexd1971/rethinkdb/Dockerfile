FROM rethinkdb
RUN apt-get update
RUN apt-get install -y python python-pip python-setuptools
RUN pip install rethinkdb
RUN apt-get remove -y python-pip
RUN apt-get -y autoremove
RUN apt-get -y clean
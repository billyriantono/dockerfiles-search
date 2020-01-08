FROM magentys/devops:latest

RUN apt-get update && apt-get install -y python-pip 

RUN mkdir /testinfra && pip install setuptools -t /testinfra && pip install distribute -t /testinfra && pip install 'git+https://github.com/magentys/testinfra@master#egg=testinfra' -t /testinfra

CMD ["/bin/bash", "-l"]

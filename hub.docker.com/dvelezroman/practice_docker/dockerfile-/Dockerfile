FROM dsbconsulting/ubuntu:14.04

RUN apt-get update
RUN apt-get install -y build-essential python-dev python-pip libyaml-dev
RUN pip install argparse 
RUN pip install stuf 
RUN pip install regex 
RUN pip install python-dateutil 
RUN pip install redis 
RUN pip install elasticsearch 
RUN pip install py4j 
RUN pip install flask 
RUN pip install mrjob

CMD [ "python"]

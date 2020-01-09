FROM python:3.6

RUN apt-get update
RUN mkdir workspace
COPY dl4us ./workspace/
RUN apt-get install -y cmake
RUN apt-get install -y swig
RUN pip install -r ./workspace/requirements.txt
RUN pip install opencv-python==3.4.2.17 --trusted-host pypi.python.org

CMD jupyter notebook ./workspace/ --port 80 --ip=0.0.0.0 --allow-root
CMD echo "plz run docker-machine ip and access http://ip:8080/?token=~~"

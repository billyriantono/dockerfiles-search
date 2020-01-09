# python:alpine is 3.{latest}
# https://github.com/sjeeva/flaskapp/blob/master/Dockerfile
# https://runnable.com/docker/python/dockerize-your-flask-application
# https://www.wintellect.com/containerize-python-app-5-minutes/

FROM python
COPY /app /app
WORKDIR /app


RUN apt-get update
RUN apt-get install -y libblas-dev liblapack-dev libatlas-base-dev gfortran

RUN pip install --upgrade pip
RUN pip install numpy
RUN pip install lxml
RUN pip install Cython
RUN pip install scikit-learn

RUN apt-get update
RUN apt-get install -y libblas-dev liblapack-dev libatlas-base-dev gfortran
RUN apt-get -y install python-lxml


RUN pip install -r requirements.txt



RUN python -m nltk.downloader -d /usr/local/share/nltk_data punkt
EXPOSE 5000
ENTRYPOINT ["python", "/app/index.py"]

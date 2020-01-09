#Container is being built in a Linux environment
FROM debian:stable

RUN useradd  -d /home/camhellstern -ms /bin/bash camhellstern

RUN mkdir -p /home/camhellstern/Documents/app
WORKDIR /home/camhellstern/Documents/app

ADD . /home/camhellstern/Documents/app

#Sets permissions for the user that will run the project.
RUN chmod -R 755 /home/camhellstern/Documents/app/06272017/particle-server
RUN chown -R camhellstern:camhellstern /home/camhellstern/Documents/app/06272017/particle-server
RUN chmod -R 777 /home/camhellstern/Documents/app/PF_Runs


#Installation of all necessary packages and libraries for the various projects that will be run
RUN apt-get update
RUN apt-get install sudo
RUN apt-get install -y sysv-rc
RUN apt-get install -y gnupg
RUN apt-get install -y gnupg2
RUN apt-get install -y wget
#RUN apt-get install -y libarmadillo-dev
#RUN apt-get install -y libcpprest-dev
#RUN apt-get install -y g++
RUN apt-get install -y python
RUN apt-get install -y mongodb
RUN apt-get install -y mongodb-server
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

RUN apt-get install -y vim

RUN apt-get install -y python-pip
RUN apt-get install -y python-pymongo
RUN echo 'deb http://www.rabbitmq.com/debian/ testing main' | tee /etc/apt/sources.list.d/rabbitmq.list
RUN wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | apt-key add -
RUN apt-get install -y rabbitmq-server
#RUN apt-get install -y python-celery
RUN apt-get install -y celeryd
RUN apt-get install -y python-flask-restful
RUN apt-get install -y python-flask-sockets
RUN apt-get install -y libarmadillo-dev
RUN apt-get install -y libcpprest-dev
RUN pip install flask-restful
RUN pip install flask-cors
RUN pip install flask-socketio
RUN pip install flask-httpauth
RUN pip install passlib
RUN pip install lxml
RUN pip install pykml
#RUN pip install bson
RUN pip install pymongo
RUN pip install requests
RUN pip install itsdangerous
RUN pip install rabbitmq
RUN pip install celery
RUN pip install numpy
RUN pip install h5py
RUN pip install eventlet

#Compiles the C++ server
RUN g++ -Wall -Wshadow -o startServer Earth.h Earth.cpp EarthEnvironment.h EarthEnvironment.cpp Euler.h Euler.cpp JTime.h JTime.cpp Particle.h Particle.cpp Particle_Filter.h Particle_Filter.cpp DataStructure.h Kalman.h Kalman.cpp server.h server.cpp main.cpp -larmadillo -lboost_system -lcrypto -lssl -lcpprest -pthread


#Exposes the various ports which allows us to connect to the container via the web browser
EXPOSE 27099
EXPOSE 27015
EXPOSE 27017
EXPOSE 5000

#This python script will run all of the separate modules in individual threads
CMD ["python", "run_project.py"]

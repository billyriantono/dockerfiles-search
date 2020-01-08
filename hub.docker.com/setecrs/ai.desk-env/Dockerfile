FROM ipeddocker/iped:3.15.6

RUN apt-get update
RUN apt-get install -y python3-pip
RUN python3 -m pip install Cython
RUN apt-get install -y openjdk-8-jdk
RUN python3 -m pip install pyjnius
RUN python3 -m pip install requests pandas 
RUN apt-get install -y python3-pyqt5
RUN python3 -m pip install scikit-image matplotlib cython scikit-learn jupyter tensorflow keras
ENV TZ=Brazil/East
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get install -y python3-opencv

ENV CLASSPATH=/root/IPED/iped/iped.jar
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

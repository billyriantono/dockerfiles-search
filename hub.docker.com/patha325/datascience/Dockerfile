# 
# docker run -it --rm -v ~/Desktop:/tf/notebooks -p 8888:8888 tensorflow/tensorflow:latest-py3-jupyter
# 

FROM tensorflow/tensorflow:latest-py3-jupyter
MAINTAINER Patrik Hallsjo

ENV DEBIAN_FRONTEND=noninteractive 

RUN apt-get update && apt-get install -y python3-pandas

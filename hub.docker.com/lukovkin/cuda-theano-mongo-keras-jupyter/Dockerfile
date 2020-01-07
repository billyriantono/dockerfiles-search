FROM lukovkin/dockerfile-cuda-keras

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 \
  && echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list \
  && apt-get update
  
RUN sudo apt-get install -y mongodb-org

RUN source activate keras \
  && conda install -y \
    jupyter \
    matplotlib \
    seaborn

VOLUME /notebook
WORKDIR /notebook
EXPOSE 8888
CMD source activate keras \
  && jupyter notebook --no-browser --ip=0.0.0.0

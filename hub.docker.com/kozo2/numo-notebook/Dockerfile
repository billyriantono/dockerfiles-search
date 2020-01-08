FROM ubuntu
RUN apt update; apt install -y git ruby gcc ruby-dev rake make
RUN cd; git clone git://github.com/masa16/numo-narray; cd numo-narray; gem build numo-narray.gemspec; gem install numo-narray-0.9.0.1.gem pry; cd

# numpy, scipy
RUN apt install -y wget python python-dev python-numpy python-scipy python-matplotlib
# jupyter, sklearn
RUN wget https://bootstrap.pypa.io/get-pip.py; python get-pip.py; pip install -U scikit-learn jupyter
# iruby
RUN apt install -y libzmq3-dev gnuplot libtool-bin autoconf g++; gem install rbczmq iruby

EXPOSE 8888
CMD iruby notebook --no-browser --ip='*' --port 8888

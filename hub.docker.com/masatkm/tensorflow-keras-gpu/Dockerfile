FROM nvidia/cuda

RUN apt update
RUN apt upgrade -y
RUN apt install python3.6 python3.6-dev -y
RUN ln -s /usr/bin/python3.6 /bin/python
RUN apt install python3-pip -y
RUN pip3 install -U jupyter
RUN pip3 install numpy scipy scikit-learn
RUN pip3 install matplotlib pandas
RUN pip3 install pydot
RUN pip3 install pillow h5py
RUN pip3 install -U tensorflow
RUN pip3 install -U keras

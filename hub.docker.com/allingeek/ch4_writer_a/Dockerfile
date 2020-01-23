FROM tensorflow/tensorflow:1.14.0-gpu-py3
MAINTAINER allentseng <allen050883@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive


RUN apt update -y;\
    apt install tzdata -y ;\

RUN apt update -y;\
    apt install git -y;\
    apt install nano -y;\
    apt-get install -y wget;\
    apt-get install python3-tk -y;\
    apt install -y libsm6 libxext6 -y;\
#    apt-get install libxrender1 -y;\
#    apt-get install libxext-dev -y

RUN pip install python3-wget;\
    pip install scipy;\
    pip install pandas;\
    pip install scikit-image;\
    pip install matplotlib;\
#    pip install opencv-python

RUN pip uninstall tensorflow-gpu -y;\
    pip uninstall tensorflow -y;\
    pip install --upgrade tensorflow-gpu==1.14
    
RUN wget https://bitbucket.org/TsengPoYen/google_draw/downloads/google_draw_1204.zip

RUN mkdir /workspace
WORKDIR /workspace

# IPython
EXPOSE 8888
# TensorBoard
EXPOSE 6006


CMD ["bash"]

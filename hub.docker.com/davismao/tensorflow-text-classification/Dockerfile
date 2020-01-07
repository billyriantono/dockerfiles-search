FROM docker.io/tensorflow/tensorflow:1.8.0-py3

RUN pip install tensorflow-hub && pip install seaborn
COPY python3-tk_3.5.3-1_amd64.deb /python3-tk_3.5.3-1_amd64.deb
RUN apt-get update && apt-get install -y libsm6 libxrender1 libxext-dev  && apt-get install -y blt && apt-get install -y libtcl8.6 && apt-get install -y  libtk8.6 && apt-get install -y libx11-6 && apt-get install -y tk8.6-blt2.5
RUN pip3 install opencv-python
RUN pip3 install Cython && pip3 install Keras && pip3 install PyWavelets && pip3 install scikit_image && pip3 install PyYAML && pip3 install scikit-image
RUN apt install /python3-tk_3.5.3-1_amd64.deb
COPY install /home/install
RUN cd /home/install/imgaug-0.2.5 && python3 setup.py install
RUN cd /home/install/imutils-0.4.6 && python3 setup.py install
RUN cd /home/install/networkx-2.1 && python3 setup.py install
RUN cd /home/install/pycocotools-2.0.0 && python3 setup.py install
RUN cd /home/install/skimage-0.0 && python setup.py install sdist
RUN mkdir /my_module_cache
ADD cmd.sh /cmd.sh 

ADD downloader.py /downloader.py

RUN chmod +x /cmd.sh

RUN /cmd.sh

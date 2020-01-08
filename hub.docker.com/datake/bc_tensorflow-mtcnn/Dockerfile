FROM tensorflow/tensorflow:1.4.1-gpu-py3
RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list
#COPY pip.conf /root/.pip/pip.confRUN chmod a+rwx /etc/bash.bashrc

RUN pip3 install opencv-contrib-python==3.2.0.8 \
                 mtcnn \
                 scikit-image \
                 tqdm
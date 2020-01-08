FROM mingjerli/ubuntuanaconda3
MAINTAINER Ming-Jer Lee <mingjerli@gmail.com>

RUN apt-get install -y libgtk2.0-0 build-essential 

RUN conda update conda
RUN conda update -y --all
RUN conda install -y -c menpo opencv3=3.1.0
RUN pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.11.0rc1-cp35-cp35m-linux_x86_64.whl
RUN pip install keras

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]
FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
MAINTAINER  whaozl <whaozl@126.com>

#install jupyter and jupyter lab and config jupyter
#you should set password by
#ipython
#from notebook.auth import passwd
#passwd() passwd default is 123456
#RUN pip3 --no-cache-dir install cntk-gpu
#config keras
#config openssh-server ssh


#CMD ln /dev/null /dev/raw1394
#CMD ["sh", "-c", "ln /dev/null /dev/raw1394 ; /etc/init.d/ssh start ; nohup jupyter lab >/dev/null 2>&1 &"]
#COPY start.sh /root/start.sh
#CMD sh /root/start.sh

RUN apt-get update && apt-get install -y \
     git \
     libopenblas-dev \
     libopencv-dev \
     python-dev \
     python-numpy \
     python-setuptools \
     python3-dev \
     python3-numpy \
     python3-setuptools \
     wget \
     vim \
     openssh-server \
     openmpi-bin \
     lrzsz \
     rar unrar zip unzip p7zip-full p7zip-rar p7zip \
  && apt-get clean \
  && echo "set fileencodings=utf-8,gb2312,gbk,gb18030\
     \nset termencoding=utf-8\
     \nset encoding=prc\
     \nset number"\
     >> /etc/vim/vimrc \
  && cd /etc/ssh \
  && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/g' sshd_config \
  && sed -i 's/#PasswordAuthentication/PasswordAuthentication/g' sshd_config \
  && sed -i 's/RhostsRSAAuthentication no/RhostsRSAAuthentication yes/g' sshd_config \
  && sed -i 's/HostbasedAuthentication no/HostbasedAuthentication yes/g' sshd_config \
  && sed -i 's/PermitEmptyPasswords no/PermitEmptyPasswords yes/g' sshd_config \
  && sed -i 's/#KerberosAuthentication no/KerberosAuthentication yes/g' sshd_config \
  && sed -i 's/#KerberosOrLocalPasswd/KerberosOrLocalPasswd/g' sshd_config \
  && sed -i 's/#KerberosTicketCleanup/KerberosTicketCleanup/g' sshd_config


# install pip2 & pip3
RUN wget https://bootstrap.pypa.io/get-pip.py --no-check-certificate \
  && python2 get-pip.py && python3 get-pip.py \
  && ln -s /usr/local/bin/pip2  /usr/bin/pip2 && ln -s /usr/local/bin/pip3  /usr/bin/pip3 \
  && ln -s /usr/bin/python3 /usr/bin/p \
  && rm get-pip.py \
  && pip2 --no-cache-dir install wheel pillow nose scipy matplotlib opencv_python protobuf \
     scikit-learn scikit-image pyyaml h5py pandas SimpleITK regex jieba openpyxl xlsxwriter xlrd tqdm asq \
     tensorflow-gpu keras  \
  && pip3 --no-cache-dir install wheel pillow nose scipy matplotlib opencv_python protobuf \
     scikit-learn scikit-image pyyaml h5py pandas SimpleITK regex jieba openpyxl xlsxwriter xlrd tqdm asq JPype1 pyhanlp \
     jupyter jupyterlab \
     tensorflow-gpu keras torch torchvision mxnet-cu90 \
  && jupyter serverextension enable --py jupyterlab --sys-prefix \
  && jupyter notebook --generate-config --allow-root \
  && echo "c.NotebookApp.ip='*'\n\
     c.NotebookApp.password=u'sha1:7de7ea9c4921:c5633014d406ce2f7cfa9a80b2be1c280fd9f42f'\n\
     c.NotebookApp.open_browser=False\n\
     c.NotebookApp.port=8888" \
     > /root/.jupyter/jupyter_notebook_config.py \
  && mkdir /root/.keras \
  && echo '{\n \
     \n"image_dim_ordering": "tf", \
     \n"epsilon": 1e-07, \
     \n"floatx": "float32", \
     \n"backend": "tensorflow" \
     \n}' \
     > /root/.keras/keras.json


WORKDIR /


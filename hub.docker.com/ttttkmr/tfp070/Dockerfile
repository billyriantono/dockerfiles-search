## FROM : DockerFileの元になるイメージを指定
FROM tensorflow/tensorflow:2.0.0b1-gpu-py3

## pip, apt-get
RUN pip install --upgrade pip
RUN pip install tensorflow-probability==0.7.0
RUN pip install matplotlib
RUN pip install pandas
RUN pip install pyqtgraph
RUN pip install pylint
RUN pip install scikit-learn
RUN pip install scipy
RUN pip install seaborn
#RUN /usr/bin/python3 -m pip install -U jupyter --user　#vscode用

RUN apt-get update
RUN apt-get install -y python3-pyqt4
RUN pip install ipython==7.6.1
RUN pip install ipython-genutils==0.2.0

## NVIDIA-Docker-envs
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES utility,compute

### 以下のenv設定はなぜか反映されない
## GUIapplication-env
ENV DISPLAY $DISPLAY
ENV QT_GRAPHICSSYSTEM "native"
ENV QT_X11_NOMITSHM 1
ENV PYTHONUNBUFFERED 1

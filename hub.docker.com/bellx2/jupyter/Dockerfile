FROM tensorflow/tensorflow:latest-py3-jupyter
RUN apt-get update
RUN apt-get install -y libsm6 libxext6 libxrender-dev
RUN apt-get install -y libglib2.0-0
RUN pip install opencv-python
RUN pip install -q keras
RUN pip install -q scikit-learn
RUN pip install -q pandas
RUN pip install -q jupyter_contrib_nbextensions
RUN pip install -q pillow
RUN jupyter contrib nbextension install --user
RUN jupyter nbextensions_configurator enable --user


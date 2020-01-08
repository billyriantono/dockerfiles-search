FROM yantonov/anaconda3

MAINTAINER Yury Antonov <yantonov@yandex.ru>

RUN pip install --ignore-installed --upgrade \
     https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.14.0-cp37-cp37m-linux_x86_64.whl

ADD files/conda_requirements.txt /
RUN conda install -y --file /conda_requirements.txt
ADD files/requirements.txt /
RUN pip install -r /requirements.txt

RUN conda clean --packages

# used by keras visualization utilities
RUN apt-get install -y \
    graphviz

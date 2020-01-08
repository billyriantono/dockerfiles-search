FROM registry.docker-cn.com/tensorflow/tensorflow:1.8.0-py3

# If you prefer miniconda:
#FROM continuumio/miniconda3

LABEL Name=deepocrservice Version=0.0.1
EXPOSE 5000

WORKDIR /app
ADD . /app

# Apt install python dependencies
RUN apt-get update && apt-get install -y libsm6 && \
    apt-get install -y libxrender1 && \
    apt-get install -y libxext-dev && \
    apt-get install -y python3-tk && \
    rm -rf /var/lib/apt/lists/*

# Using pip:
RUN pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/ --no-cache-dir

# Build ctpn libs
RUN cd tf_ctpn/lib && make


CMD ["python", "app.py"]

# Using pipenv:
#RUN python3 -m pip install pipenv
#RUN pipenv install --ignore-pipfile
#CMD ["pipenv", "run", "python3", "-m", "deepocrservice"]

# Using miniconda (make sure to replace 'myenv' w/ your environment name):
#RUN conda env create -f environment.yml
#CMD /bin/bash -c "source activate myenv && python3 -m deepocrservice"

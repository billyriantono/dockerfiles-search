FROM tensorflow/tensorflow:latest-gpu-py3

MAINTAINER kths

RUN pip install tensorflow-probability sklearn matplotlib optuna jupyter pystan

WORKDIR /home 
EXPOSE 11111
ENTRYPOINT ["jupyter", "notebook", "--port=11111", "--no-browser", "--allow-root", "--ip=0.0.0.0", "--NotebookApp.token='kths321' "]


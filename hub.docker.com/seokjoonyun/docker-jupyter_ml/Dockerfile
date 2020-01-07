# Made by seokjoon.yun (seokjoon.yun@gmail.com)
# Distributed under the terms of the Modified MIT License.


# jupyter/scipy-notebook by Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/scipy-notebook

LABEL maintainer="seokjoon.yun<seokjoon.yun@gmail.com>"

USER root

# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH

ENV LANG C.UTF-8

RUN pip install --upgrade pip
RUN conda install xgboost lightgbm catboost seaborn s3fs pyarrow boto3 keras pymysql slacker -y -c conda-forge
RUN pip install sklearn
# RUN pip install sagemaker df2gspread

#########################################
# Copy your notebook file to docker image
#########################################

#COPY [your notebok directory] notebook
#RUN chmod -R 777 notebook

########################################
# run your notebook file on docker image
######################################## 
#RUN jupyter nbconvert --execute notebook/[YOUR NOTEBOOK FILE].ipynb --ExecutePreprocessor.timeout=-1 --to markdown --stdout


##############################
# CMD for run Jupyter Notebook
##############################
#docker run -it -p :8888:8888 conda-ml:latest

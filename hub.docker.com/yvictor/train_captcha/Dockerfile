# Created on Dec, 8, 2016
# @author: Yvictor

FROM yvictor/keras_tensorflow:0.10.0-gpu
MAINTAINER yvictor


COPY . /train_captcha
WORKDIR /train_captcha

ENV PATH /root/miniconda3/bin:$PATH

RUN source activate intelpy3
RUN ipython notebook -p 8889

CMD python train.py 

FROM continuumio/anaconda3
ENV LANG C.UTF-8

RUN apt-get clean && apt-get update && \
    apt-get install -y libgl1-mesa-dev && \
    conda install -y -c conda-forge opencv && \
    pip install tensorflow tqdm h5py keras kaggle-cli gym chainer pymysql ipython-sql && \
    conda install pytorch torchvision -c soumith

CMD ["/bin/bash"]

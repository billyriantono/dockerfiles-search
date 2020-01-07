FROM pytorch/pytorch:1.2-cuda10.0-cudnn7-runtime

WORKDIR /workspace
ADD http://mitra.stanford.edu/kundaje/surag/docker_files.tar.gz /workspace/
RUN tar -xvzf ./docker_files.tar.gz
RUN mv docker_files/* .
RUN rm -rf docker_files.tar.gz docker_files

RUN apt-get update && apt-get install -y --no-install-recommends \
         wget \
         screen \
         vim \
         htop \
         man \
         tabix && \
     rm -rf /var/lib/apt/lists/*

RUN conda install -y -c bioconda pysam pyfaidx
RUN conda install -y scikit-learn pandas
RUN pip install tensorboard future 

RUN chmod 777 /var/run/screen/
RUN chmod -R a+w .

FROM continuumio/anaconda3:5.3.0

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install htop -y
RUN apt-get install procps -y
RUN conda update conda -y
RUN conda install -y gdal=3.0.2
RUN conda install -y aiohttp=3.6.2
RUN pip install s2cloudless==1.3.0

WORKDIR /opt
RUN wget http://step.esa.int/thirdparties/sen2cor/2.5.5/Sen2Cor-02.05.05-Linux64.run
RUN chmod 755 Sen2Cor-02.05.05-Linux64.run
RUN bash Sen2Cor-02.05.05-Linux64.run
RUN rm Sen2Cor-02.05.05-Linux64.run
RUN echo 'PATH=$PATH:/opt/Sen2Cor-02.05.05-Linux64/bin' >> ~/.bashrc
RUN bash -c 'source ~/.bashrc'  

WORKDIR /root
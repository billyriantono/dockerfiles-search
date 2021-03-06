#FROM alpine as intermediate
#RUN apk add --no-cache git openssh 
## add credentials on build
#ARG SSH_PRIVATE_KEY
#RUN mkdir /root/.ssh/
#RUN echo "${SSH_PRIVATE_KEY}" > /root/.ssh/id_rsa
#RUN chmod 400 /root/.ssh/id_rsa
## make sure tha domain is accepted
#RUN touch /root/.ssh/known_hosts
#RUN ssh-keyscan github.com >> /root/.ssh/known_hosts
#
#RUN git clone --depth=1 git@github.com:seung-lab/BigArrays.jl.git BigArrays 
#RUN git clone --depth=1 git@github.com:seung-lab/ChunkFlow.jl.git -b inference-script ChunkFlow
#

#FROM nvidia/cuda:8.0-cudnn6-runtime-ubuntu16.04
#FROM jingpengw/kaffe
FROM seunglab/kaffe:pznet
#FROM nvidia/cuda:8.0-cudnn5-runtime-ubuntu14.04
LABEL   maintainer="Jingpeng Wu" \
        project="ChunkFlow"


#### update repository
RUN apt update 
#RUN apt install -y -qq --no-install-recommends software-properties-common
#RUN add-apt-repository main
#RUN add-apt-repository universe
#RUN add-apt-repository restricted
#RUN add-apt-repository multiverse
#RUN add-apt-repository ppa:staticfloat/julia-deps 
#RUN apt-get update
       
#### install some packages
RUN apt-get install -qq --no-install-recommends build-essential wget unzip libjemalloc-dev libhdf5-dev libblosc-dev libmagickwand-6.q16-2 python-dev python-pip ssh 
RUN pip install --upgrade pip
RUN pip install -U setuptools 
RUN pip install awscli gsutil  
#RUN pip install protobuf google cloud-volume

ENV LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so 

# install gcloud
ENV PATH /opt/google-cloud-sdk/bin:$PATH
RUN pip install -U crcmod
RUN mkdir -p /opt/gcloud && \
    wget --no-check-certificate --directory-prefix=/tmp/ https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.zip && \
    unzip /tmp/google-cloud-sdk.zip -d /opt/ && \
    /opt/google-cloud-sdk/install.sh --usage-reporting=true --path-update=true --bash-completion=true --rc-path=/opt/gcloud/.bashrc --disable-installation-options && \
    gcloud --quiet components update app preview alpha beta app-engine-java app-engine-python kubectl bq core gsutil gcloud && \
    rm -rf /tmp/*
#RUN gcloud auth activate-service-account --key-file /secrets/google-secret.json 

#### install julia
WORKDIR /opt 
RUN wget https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.2-linux-x86_64.tar.gz 
RUN tar -xvf julia-0.6.2-linux-x86_64.tar.gz
RUN mv julia-d386e40c17 julia-0.6
ENV JULIA_PATH /opt/julia-0.6 
ENV JULIA_VERSION 0.6.2
ENV PATH $JULIA_PATH/bin:$PATH

# Julia computational environment
RUN julia -e 'Pkg.init()'
RUN julia -e 'Pkg.update()'

#WORKDIR /root/.julia/v0.6
#COPY --from=intermediate /root/BigArrays  BigArrays 
#COPY --from=intermediate /root/ChunkFlow  ChunkFlow 

RUN julia -e 'Pkg.clone("https://github.com/JuliaWeb/HTTP.jl.git")'
RUN julia -e 'Pkg.clone("https://github.com/jingpengw/GoogleCloud.jl.git")'
#RUN julia -e 'Pkg.clone("https://github.com/JuliaCloud/AWSCore.jl.git")'
RUN julia -e 'Pkg.clone("https://github.com/jingpengw/AWSCore.jl.git")'
RUN julia -e 'Pkg.clone("https://github.com/jingpengw/AWSSQS.jl.git")'
RUN julia -e 'Pkg.clone("https://github.com/samoconnor/AWSS3.jl.git")'
RUN julia -e 'Pkg.clone("https://github.com/JuliaCloud/AWSSDK.jl.git")'
RUN julia -e 'Pkg.clone("https://github.com/seung-lab/EMIRT.jl.git")'
#RUN julia -e 'Pkg.clone("https://github.com/seung-lab/BigArrays.jl.git")'
#RUN julia -e 'Pkg.clone("https://github.com/seung-lab/GSDicts.jl.git")'
#RUN julia -e 'Pkg.clone("https://github.com/seung-lab/S3Dicts.jl.git")'
#RUN julia -e 'Pkg.clone("https://github.com/seung-lab/BOSSArrays.jl.git")'
#RUN julia -e 'Pkg.clone("https://github.com/seung-lab/CloudVolume.jl.git")'
#RUN julia -e 'Pkg.clone("https://github.com/seung-lab/ChunkFlow.jl.git")'

# RUN julia -e 'Pkg.checkout("CloudVolume", "julia0.6")'
#RUN julia -e 'Pkg.checkout("ChunkFlow", "inference-script")'
#RUN julia -e 'Pkg.build("ChunkFlow")'
#RUN julia -e 'using ChunkFlow'
#RUN julia -e 'Pkg.test("BigArrays")'


ENTRYPOINT bash
#WORKDIR /root/.julia/v0.6/ChunkFlow/scripts

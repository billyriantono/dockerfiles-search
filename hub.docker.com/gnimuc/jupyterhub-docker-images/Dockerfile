# rebuild
FROM debian:jessie

MAINTAINER Gnimuc Key <GnimucKey@gmail.com>

# dependencies
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -yq --no-install-recommends \
    git \
    vim \
    wget \
    build-essential \
    python-dev \
    ca-certificates \
    bzip2 \
    unzip \
    libsm6 \
    pandoc \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    supervisor \
    sudo \
    npm nodejs-legacy \
    curl \
    && apt-get clean

# install conda
ENV PATH /opt/conda/bin:$PATH
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    /bin/bash /Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda && \
    rm Miniconda3-latest-Linux-x86_64.sh && \
    /opt/conda/bin/conda install --yes conda

# jupyterhub dependencies
RUN npm install -g configurable-http-proxy

# single-user jupyter
RUN conda install jupyter

# install jupyterhub
RUN pip install jupyterhub

# change DIR
WORKDIR /root

# install julia v0.4.0 system-wide
RUN mkdir -p /opt/julia_0.4.0 && \
    curl -s -L https://julialang.s3.amazonaws.com/bin/linux/x64/0.4/julia-0.4.0-linux-x86_64.tar.gz | tar -C /opt/julia_0.4.0 -x -z --strip-components=1 -f -
RUN ln -sf /opt/julia_0.4.0/bin/julia /usr/local/bin/
# make a julia global packages directory and add it to LOAD_PATH
RUN mkdir /opt/global-packages
RUN echo 'push!(LOAD_PATH, "/opt/global-packages/.julia/v0.4/")' >> /opt/julia_0.4.0/etc/julia/juliarc.jl
ENV JULIA_PKGDIR /opt/global-packages/.julia/

# install "IJulia" system-wide
RUN julia -e 'Pkg.init()'
RUN julia -e 'Pkg.add("IJulia")'
RUN julia -e 'Pkg.build("IJulia")'    # I don't know why the kernel of IJulia won't be installed without build it again.
# move kernelspec from gnimuc's jupyter to global jupyter
RUN cd /usr/local/share/ && mkdir -p jupyter/kernels/
#RUN cp -r /root/.local/share/jupyter/kernels/julia-0.4 /usr/local/share/jupyter/kernels/
RUN jupyter kernelspec install /root/.local/share/jupyter/kernels/julia-0.4 

# install "Images"
RUN apt-get update && apt-get install -yq --no-install-recommends \
    gettext \
    tcl8.5 \
    libmagickwand-6.q16-2 \
    libcairo2 \
    libpango1.0-0 \
    tk8.5 \
    && apt-get clean   

RUN julia -e 'Pkg.add("Images")' 
RUN julia -e 'Pkg.update()' 

# download  RISE and pre-install
RUN git clone https://github.com/damianavila/RISE
RUN mkdir -p .jupyter && cd RISE && python setup.py install

# add admin
RUN useradd -d /home/admin -m admin; \
    echo "admin:admin" | chpasswd; \
    adduser admin sudo
RUN chown -R admin /home/admin

# add users
RUN useradd -d /home/gnimuc -m gnimuc; \
    echo "gnimuc:gnimuc" | chpasswd; \
    adduser gnimuc sudo

# install RISE for gnimuc
RUN mkdir -p /home/gnimuc/.local/share/jupyter && mkdir -p /home/gnimuc/.jupyter
RUN cp -r /root/.local/share/jupyter/nbextensions /home/gnimuc/.local/share/jupyter/
RUN cd RISE && JUPYTER_CONFIG_DIR=/home/gnimuc/.jupyter python setup.py install

# give user permisstion
RUN chown -R gnimuc /home/gnimuc


# expose ports
EXPOSE 8000

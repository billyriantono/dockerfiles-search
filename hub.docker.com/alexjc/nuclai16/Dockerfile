FROM ubuntu:14.04

# Install dependencies
RUN apt-get -qq update           &&  \
    apt-get -qq install --assume-yes \
        "build-essential"           \
        "git"                       \
        "vim"                       \
        "zip"                       \
        "wget"                      \
        "pkg-config"             &&  \
    rm -rf /var/lib/apt/lists/*

# Miniconda.
RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.0.5-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

# Install requirements before copying project files
WORKDIR /lstm
RUN /opt/conda/bin/conda install -q -y conda numpy pip h5py
RUN /opt/conda/bin/python3 -m pip install theano==0.8.2 keras==1.0.3
RUN /opt/conda/bin/python3 -m pip install git+https://github.com/farizrahman4u/seq2seq 
RUN unlink python; ln -s /opt/conda/bin/python3 /bin/python

# Copy only required project files
COPY data.py .
COPY tweet.py .
COPY s2s.py .
COPY reply.py .

# Pre-trained network.
RUN wget -q "https://github.com/aigamedev/nuclai16/releases/download/0.0/lstm512.zip"
RUN wget -q "https://github.com/aigamedev/nuclai16/releases/download/0.0/lstm256x3.zip"
RUN wget -q "https://github.com/aigamedev/nuclai16/releases/download/0.0/tweets78k.txt.bz2"
RUN bunzip2 tweets78k.txt.bz2 ; unzip lstm512.zip ; unzip lstm256x3.zip ; rm *.zip

# Set an entrypoint to the main doodle.py script
ENTRYPOINT ["/bin/bash"]

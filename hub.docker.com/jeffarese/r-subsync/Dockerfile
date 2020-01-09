FROM ubuntu
RUN apt update
RUN apt install -y wget
RUN apt install -y git
RUN apt install -y python3
RUN apt install -y python3-pip
RUN alias python=python3
RUN apt install -y ffmpeg
RUN mkdir /workspace/
RUN wget -O /workspace/rSubsync.py https://github.com/jeffarese/r-subsync/raw/master/rsubsync.py
RUN pip3 install git+https://github.com/smacke/subsync
RUN ls /workspace
RUN echo "alias rsubs=\"python3 /workspace/rSubsync.py\"" >> ~/.bashrc 
RUN /bin/bash -c "source ~/.bashrc"

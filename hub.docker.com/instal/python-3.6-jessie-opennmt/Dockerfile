FROM python:3.6-jessie

ENV TERM xterm-256color
ENV PYTHONUNBUFFERED 1
ENV PYTHONPATH "${PYTHONPATH}:/docker/application/src/"

# Set the default workdir in the env so to access it in the project if needed
ENV WORKDIR /docker/application
WORKDIR $WORKDIR

# requirements
RUN git clone https://github.com/OpenNMT/OpenNMT-py.git --branch v0.1
RUN pip install torchtext==0.2.3
RUN pip install -r OpenNMT-py/requirements.txt
RUN pip install numpy==1.15.2
RUN pip install torch==0.3.1
FROM debian:stretch
MAINTAINER Alex, Jiang <alexxyjiang@gmail.com>
ENV LANG=C.UTF-8
RUN apt update --fix-missing \
    && apt install -y build-essential cmake exuberant-ctags git \
    && apt install -y python3 python3-dev python3-pip python3-tk
RUN useradd -m -g users -s /bin/bash bloguser
USER bloguser
COPY ./requirements.txt /home/bloguser/requirements.txt
RUN pip3 install --upgrade pip
ENV PATH=$PATH:/home/bloguser/.local/bin
RUN pip install --user --upgrade --requirement /home/bloguser/requirements.txt
CMD ["/bin/bash"]

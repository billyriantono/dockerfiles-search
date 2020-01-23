FROM ubuntu:18.04
MAINTAINER chaunecy <chaunecy@outlook.com>

RUN apt-get update && \
    apt-get install wget -y && \
    apt-get install python3.6 -y && \
    apt-get install python3.6-dev -y && \
    apt-get install python3.6-venv -y && \
    apt-get install python3-distutils -y && \
    wget https://bootstrap.pypa.io/get-pip.py -O - | python3.6 && \
    apt-get remove wget -y && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    rm -f /usr/bin/python && \
    rm -f /usr/bin/python3 && \
    ln -s /usr/bin/python3.6 /usr/bin/python && \
    ln -s /usr/bin/python3.6 /usr/bin/python3 && \
    rm -rf /var/lib/apt/lists/* && \
    useradd guest -m && \
    chmod a-w /home/guest/.bashrc && \
    chmod a-w /home/guest/.profile && \
    chmod a-w /home/guest/.bash_logout

USER guest
WORKDIR home
WORKDIR guest
EXPOSE 80
CMD ["bash"]

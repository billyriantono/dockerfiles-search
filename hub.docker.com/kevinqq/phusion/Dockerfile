FROM phusion/baseimage:0.10.0
LABEL author="kevinqq"

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# ...put your own build instructions here...


#代码复制过来后的路径
RUN mkdir /code
WORKDIR /code

#安装需要的python库
RUN apt-get update
RUN apt-get install -y wget

#安装python3.6 来自第三方
RUN add-apt-repository ppa:jonathonf/python-3.6
RUN apt-get update
RUN apt-get install -y python3.6
#RUN apt install -y python3.6-dev
#RUN apt install -y python3.6-venv
#为3.6安装pip
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python3.6 get-pip.py
#和自带的3.5共存
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2
RUN update-alternatives --config python3
#print()时在控制台正常显示中文
ENV PYTHONIOENCODING=utf-8

RUN pip3 install flask


# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#RUN cp /c/Users/git/docker/hello.py /code
#RUN export LANG=C.UTF-8
#RUN export FLASK_APP=hello.py
#EXPOSE 5000
#ENV LANG C.UTF-8
#CMD exec python3 /root/hello.py

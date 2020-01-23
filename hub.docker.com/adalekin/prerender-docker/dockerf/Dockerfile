#FROM python:3.6.8-alpine3.9
FROM ubuntu
LABEL maintainer="Abhinav A V <abhai2k@gmail.com>"

RUN apt update
RUN apt upgrade -y
RUN apt install python3-pip curl git -y
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt install nodejs -y
RUN pip3 install -U marshmallow
RUN git clone https://github.com/timkpaine/paperboy.git
WORKDIR paperboy/
RUN make install
WORKDIR ~
RUN rm -rf paperboy
RUN apt autoremove -y
RUN apt clean all -y

EXPOSE 8080
CMD ["python3", "-m", "paperboy.server"]
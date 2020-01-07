FROM python:3.5.4-jessie

WORKDIR /app
RUN pip install tensorflow

RUN echo 'export PS1="\n\n>> tensorflow \W \$ "' >> /root/.bashrc
ENV TERM linux
ENV TF_CPP_MIN_LOG_LEVEL 2

ENTRYPOINT bash
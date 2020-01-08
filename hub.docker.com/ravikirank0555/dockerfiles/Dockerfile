FROM ravikirank0555/dockerfiles:cu9_cdnn7_tf110_ana520py2

MAINTAINER Ravi Kiran Kummamuru <rkummamu@gmail.com>

ENV WORK_DIR /home/rk/docs/projects
WORKDIR $WORK_DIR/

RUN pwd
RUN pip install --upgrade pip
RUN git clone https://github.com/openai/gym.git
WORKDIR $WORK_DIR/gym
RUN pwd
RUN pip install -e '.[all]'

WORKDIR $WORK_DIR/



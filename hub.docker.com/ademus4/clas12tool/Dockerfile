FROM ademus4/root-6-14:latest
USER root
WORKDIR /work
ENV HOME /work

# set environment variables
ENV ROOTSYS /usr/local/bin/root
ENV CLAS12TOOL /work/Clas12Tool/
ENV DISPLAY=:0.0 \
    DISPLAY_WIDTH=1024 \
    DISPLAY_HEIGHT=768 \
    RUN_XTERM=yes \
    RUN_FLUXBOX=yes

# open vnc port
EXPOSE 8080

# install general software
RUN yum install -y nano

# install requirements for novnc server
RUN yum install -y fluxbox \
    novnc \
    x11vnc \
    xterm \
    xvfb \
    socat \
    supervisor \
    net-tools

# HIPO
RUN git clone --recurse-submodules https://github.com/dglazier/Clas12Tool.git \
&& cd Clas12Tool \
&& git checkout mesonex4
RUN cd Clas12Tool/Lz4 && make

# general environment variables
COPY environment.sh .

# make sure the work directory can be modified by any user
RUN chmod -R 777 /work

# set some aliases for clas12tools
ENV clas12reader "root -l $CLAS12TOOL/RunRoot/importToROOT.C"
ENV hipodraw "root -l $CLAS12TOOL/RunRoot/hiporoot/LoadHipoROOT.C"


# run the commands to precompile (for speed)
RUN root -l $CLAS12TOOL/RunRoot/importToROOT.C
RUN root -l $CLAS12TOOL/RunRoot/hiporoot/LoadHipoROOT.C

# run novnc server
COPY . /app
CMD ["/app/entrypoint.sh"]

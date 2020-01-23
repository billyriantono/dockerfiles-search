FROM amytabb/docker_ubuntu16_opencv4

#environment variable names
ENV NAME THRESH
ENV NAME CONVERSION_TYPE
ENV NAME DO_DEMO
ENV NAME DO_DEMO_STACK
ENV NAME DO_DEMO_XYZ
ENV NAME DO_DEMO_CC
ENV NAME CC_FLAG
RUN mkdir /write_directory
ARG DIRECTORY=write_directory
ENV VAR_DIR=$DIRECTORY


#grab the repo from github.
RUN git clone https://github.com/amy-tabb/CurveSkel-Tabb-Medeiros-2018.git
COPY run_curve_skel.sh /run_curve_skel.sh
COPY build_curve_skel.sh /build_curve_skel.sh
WORKDIR CurveSkel-Tabb-Medeiros-2018/

#compile and link
RUN /bin/sh ./../build_curve_skel.sh
WORKDIR /
CMD ["/bin/sh", "/run_curve_skel.sh"]


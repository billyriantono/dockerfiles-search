FROM amytabb/docker_ubuntu16_opencv4

#environment variable names
ENV NAME THRESH
ENV NAME TRIGGERSTACK
ENV NAME DO_DEMO
ENV NAME DO_DEMO_STACK
RUN mkdir /write_directory
ARG DIRECTORY=write_directory
ENV VAR_DIR=$DIRECTORY

#grab the repo from github.
RUN git clone https://github.com/amy-tabb/CurveSkel-Tabb-Medeiros.git
COPY run_curve_skel.sh /run_curve_skel.sh
COPY build_curve_skel.sh /build_curve_skel.sh
WORKDIR CurveSkel-Tabb-Medeiros/

#compile and link
RUN /bin/sh ./../build_curve_skel.sh
#RUN g++ src/*.cpp -o curve_skel -fopenmp -std=gnu++11 -Wall -I/usr/local/include -lgomp -lopencv_core -lopencv_imgproc -lopencv_imgcodecs
WORKDIR /
CMD ["/bin/sh", "/run_curve_skel.sh"]


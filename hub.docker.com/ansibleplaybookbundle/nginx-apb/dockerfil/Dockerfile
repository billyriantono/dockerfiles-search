FROM anosnowhong/pcl-qt-opencv

RUN apt update && apt install cmake build-essential libboost-all-dev -y \
&& apt install python-catkin-pkg -y \
&& apt install python-empy python-sip sip-dev -y \
&& apt install libprotobuf-dev protobuf-compiler libpoco-dev libeigen3-dev libtinyxml-dev liblz4-dev libbz2-dev -y \
&& apt-get install -y graphviz \
&& apt-get install -y uuid-dev \
&& apt-get install -y python-nose \
&& apt-get install -y libpcl1.7 \
&& apt-get install -y sbcl \
&& apt-get install -y liblog4cxx10-dev \
&& apt-get install -y python-paramiko \
&& apt-get install -y python-imaging \
&& apt-get install -y gstreamer0.10-plugins-good \
&& apt-get install -y python-netifaces \
&& apt-get install -y libvtk-java \
&& apt-get install -y python-opencv \
&& apt-get install -y python-coverage \
&& apt-get install -y libgstreamer-plugins-base0.10-0 \
&& apt-get install -y python-vtk6 \
&& apt-get install -y python-numpy \
&& apt-get install -y libgstreamer0.10-0 \
&& apt-get install -y libopencv-dev \
&& apt-get install -y libogg-dev \
&& apt-get install -y libapr1-dev \
&& apt-get install -y libconsole-bridge-dev \
&& apt-get install -y libcppunit-dev \
&& apt-get install -y libtheora-dev \
&& apt-get install -y libpcl-dev \
&& apt-get install -y libgstreamer-plugins-base0.10-dev \
&& apt-get install -y festvox-kallpc16k \
&& apt-get install -y libgstreamer0.10-dev \
&& apt-get install -y festival \
&& apt-get install -y libyaml-cpp-dev \
&& apt-get install -y libaprutil1-dev \
&& apt-get install -y libgtest-dev \

&& apt-get install -y python-rospkg \
&& apt-get install -y catkin \
&& ln -s /usr/lib/x86_64-linux-gnu/libvtkCommonCore-6.2.so /usr/lib/libvtkproj4.so \
&& rm -rf /tmp/* /var/lib/apt/lists/* /root/.cache/*

RUN apt update && apt install git \
&& git clone https://github.com/ApolloAuto/apollo-platform \
&& cd apollo-platform/ros \
&& cd third_party && bash build.sh \
&& cd .. && rm third_party/lib_x86_64/librosconsole* && ./build.sh build \
&& cd third_party/swig_wrapper && bash build.sh 
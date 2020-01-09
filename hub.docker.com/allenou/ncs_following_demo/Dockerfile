FROM duckietown/rpi-duckiebot-base

#COPY qemu-arm-static /usr/bin/qemu-arm-static 

RUN [ "cross-build-start" ]

RUN mkdir /home/software/ncsdk
COPY ncsdk /home/software/ncsdk
WORKDIR /home/software/ncsdk
RUN make install

WORKDIR /home/software/catkin_ws/src/
RUN git clone https://github.com/ARG-NCTU/ncs_lane_following.git 
RUN /bin/bash -c "cd /home/software/ && source environment.sh && cd catkin_ws && catkin_make --pkg ncs_following"

RUN [ "cross-build-end" ]

WORKDIR /home/software/
COPY run_ncslanefollowingdemo.sh .

CMD [ "/bin/bash run_ncslanefollowingdemo.sh" ]

FROM gdwyer/ros-base:base

### Envrionment config
ENV	INST_SCRIPTS=$HOME/install 

USER root
### Add all install scripts for further steps
ADD ./scripts/ $INST_SCRIPTS/
RUN find $INST_SCRIPTS -name '*.sh' -exec chmod a+x {} +

### Install some common tools
RUN $INST_SCRIPTS/ros_web_tools.sh

USER user
RUN $INST_SCRIPTS/setup_ros_web_tools.sh

CMD ["bash"]

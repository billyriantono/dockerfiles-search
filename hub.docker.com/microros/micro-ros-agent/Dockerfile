FROM microros/base:dashing

WORKDIR /uros_ws
RUN . /opt/ros/$ROS_DISTRO/setup.sh && . install/local_setup.sh && ros2 run micro_ros_setup create_agent_ws.sh && colcon build

# setup entrypoint
COPY ./micro-ros_entrypoint.sh /
ENTRYPOINT ["/bin/sh", "/micro-ros_entrypoint.sh"]
CMD ["--help"]

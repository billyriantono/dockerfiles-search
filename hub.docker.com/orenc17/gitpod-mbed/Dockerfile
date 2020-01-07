FROM gitpod/workspace-full:latest

USER root
COPY ./install_pip_pack.sh /tmp/
RUN /tmp/install_pip_pack.sh

USER gitpod
COPY ./install_gcc_arm.sh /home/gitpod/
RUN /home/gitpod/install_gcc_arm.sh
ENV PATH="/home/gitpod/gcc-arm-none-eabi-8-2018-q4-major-linux/bin:${PATH}"

USER root

# Dockerfile for building a cross developing environment for Qt
# targeting Windows. It also builds the application in the current
# directory. The application will be statically linked against
# Qt.
#
# To build the environment invoke
#  docker build -t qt .
# in the directory of this file. This creates a docker image
# called "qt". Note that it will take a while if you are building
# this image the first time. The contained application will also
# be compiled (in principle the last step could be done within
# the running container).
#
# Once build, you can enter the container via
#  docker run qt -ti bash
#
# (c) 2018 by Jan Hák
#
# Note that Docker requires a relatively recent Linux kernel.
# 3.8 is the current minimum.
#

FROM java:8-jdk

EXPOSE 8080

RUN git clone https://payne-x6@bitbucket.org/payne-x6/state-bank.git org.liberland.statebank

#RUN sudo mysql -u root


WORKDIR org.liberland.statebank

RUN ./gradlew bootJar

# Now build the project
CMD ./gradlew bootRun



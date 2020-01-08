########################################################################################################################
# Dockerfile to build an CentOS 7 Linux with OpenJDK 1.8
#
# Based on Centos Linux oficial image provided by hub.docker.com
#
# Usage (Image Build Command): docker build --rm -t jmzuazo/centos .
# Usage (Container Run Command): docker run -d -it jmzuazo/centos /bin/bash
# Usage (Container Attach Command): docker attach centos
#
########################################################################################################################


# Set the base image to CentOS 7 Linux
# The FROM instruction sets the Base Image for subsequent instructions
# Usage: FROM <image>
# Usage: FROM <image>:<tag>
# Usage: FROM <image>@<digest>
FROM centos:7


# The MAINTAINER instruction allows you to set the Author field of the generated images
# Usage: MAINTAINER [name] <email>
MAINTAINER Jose Matias Zuazo jmzuazo@gmail.com


# The ENV instruction sets the environment variable <key> to the value <value>.
# This value will be in the environment of all “descendent” Dockerfile commands
# and can be replaced inline in many as well.
# Usage: ENV <key> <value>
# Usage: ENV <key>=<value> ...


################## BEGIN INSTALLATION ######################

# The COPY instruction copies new files or directories from <src> and adds them to the
# filesystem of the container at the path <dest>
# Usage: COPY <src>... <dest>
# Usage: COPY ["<src>"... "<dest>"] (this form is required for paths containing whitespace)

# The RUN instruction will execute any commands in a new layer on top of the current
# image and commit the results. The resulting committed image will be used for the next step in the Dockerfile
# Usage: RUN <command> (the command is run in a shell - /bin/sh -c - shell form)
# Usage: RUN ["executable", "param1", "param2"] (exec form)

# Install OpenJDK 1.8
# Clean repositories cached files
RUN yum -y install java-1.8.0-openjdk-devel && \
    yum clean all

##################### INSTALLATION END #####################


# The EXPOSE instructions informs Docker that the container will listen on the specified network ports at runtime.
# If is not specified, use the parent image ports
# Usage: EXPOSE <port> [<port>...]


# An ENTRYPOINT allows you to configure a container that will run as an executable
# If is not specified, use the parent image entrypoint
# Usage: ENTRYPOINT ["executable", "param1", "param2"] (the preferred exec form)
# Usage: ENTRYPOINT command param1 param2 (shell form)


# The main purpose of a CMD is to provide defaults for an executing container.
# These defaults can include an executable, or they can omit the executable, in which
# case you must specify an ENTRYPOINT instruction as well.
# Usage: CMD ["executable","param1","param2"] (exec form, this is the preferred form)
# Usage: CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
# Usage: CMD command param1 param2 (shell form)

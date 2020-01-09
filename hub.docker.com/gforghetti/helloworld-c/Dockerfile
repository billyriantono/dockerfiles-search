#################################################################################################################################################
# This Dockerfile builds a simple HelloWorld Application written in the C Programming Language in a Linux Docker Image.
#################################################################################################################################################
# Gary Forghetti
# Docker Inc.
#################################################################################################################################################

FROM alpine:latest
ARG BUILDDIR="/HelloWorld"
WORKDIR ${BUILDDIR}

#################################################################################################################################################
# Add some metadata to the docker image
#################################################################################################################################################
LABEL description="HelloWorld C Application"
LABEL maintainer="Gary Forghetti, Docker Inc."

#################################################################################################################################################
# Execute the HelloWorld C Program when a container from this docker image is run.
#################################################################################################################################################
CMD /HelloWorld/HelloWorld

#################################################################################################################################################
# Copy the HelloWord.c source application into the Build Directory.
#################################################################################################################################################
COPY ./HelloWorld.c ${BUILDDIR}

#################################################################################################################################################
# Install the C Compiler, Development Libraries and Header Files.
# Compile the HelloWorld.c Program and create the executable binary.
# Erase the HelloWorld.c source code.
# Remove the C Compiler, Development Libraries and Header Files.
# Clear the alpine package cache.
#################################################################################################################################################
RUN apk update && \
apk add gcc libc-dev && \
gcc HelloWorld.c -o HelloWorld && \
chmod ugo+rx HelloWorld && \
rm -f HelloWorld.c && \
apk del gcc libc-dev && \
{ apk cache clean --purge > /dev/null @>&1 || true; }

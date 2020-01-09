FROM miles990/kbengine-get-source

MAINTAINER AlexLee <alexlee7171@gmail.com>

# Build source
WORKDIR /kbengine/kbe/src

RUN make

# Define mountable directories.
VOLUME ["/kbengine"]

EXPOSE 3306
EXPOSE 80

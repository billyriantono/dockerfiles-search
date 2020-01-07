FROM fedora:26

MAINTAINER John Doe

# Compilation parameters.
ENV BRANCH "swift-4.0-branch"

# Update the system.
RUN dnf update -y

# Install development tools.
RUN dnf groupinstall -y "C Development Tools and Libraries"

# Install build dependencies.
RUN dnf install -y git cmake ninja-build clang python libuuid-devel \
  libicu-devel libbsd-devel libedit-devel libxml2-devel libsq3-devel \
  swig python3-libs ncurses-devel pkg-config libblkid-devel \
  libcurl-devel autoconf libtool systemtap-sdt-devel tzdata

# Create a directory for Swift sources.
RUN mkdir ~/source && cd ~/source

# Clone the repo.
RUN git clone https://github.com/apple/swift.git
RUN ./swift/utils/update-checkout --scheme $BRANCH --clone

# Build Swift with optimizations and basic tests with Ninja.
RUN ./swift/utils/build-script -r -t --jobs 1

# Debug.
RUN ls && ls ./swift

# Install nginx and make compiled files available publicly.
RUN dnf install -y nginx
RUN cp -r ~/source /usr/share/nginx/html

# Expose ports.
EXPOSE 80

# Start the server.
CMD ["systemctl", "start", "nginx"]

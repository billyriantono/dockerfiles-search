FROM dnoliver/mraa-base

# Update apt-get
RUN apt-get -y update && apt-get -y --no-install-recommends install \
  # Python 2 Build Dependencies
  python python-dev python-pip \
  # Python 3 Build Dependencies
  python3 python3-dev \
  # Docs Build Dependencies
  python-sphinx

# Install virtualenv
RUN pip install virtualenv

# Set Workdir
WORKDIR $MRAA_SRC_DIR

CMD bash

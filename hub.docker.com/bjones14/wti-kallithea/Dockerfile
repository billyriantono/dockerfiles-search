FROM ubuntu

# Install packages
RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    git \
    libffi-dev \
    locales \
    mercurial \
    npm \
    python-pip \
    python-virtualenv \
    python-dev

# Set the locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8

# Clone the latest stable version
RUN hg clone https://kallithea-scm.org/repos/kallithea /kallithea-repo -r stable
WORKDIR /kallithea-repo

# Setup virtual environment
ENV VIRTUAL_ENV=/kallithea-venv
RUN python2 -m virtualenv --python=/usr/bin/python2 $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Run the install with pip, set compile catalog for translation.
RUN pip install --upgrade pip setuptools
RUN pip install --upgrade -e .
RUN python setup.py compile_catalog

# Initialize Kallithea
RUN kallithea-cli front-end-build

# Remove the working directory of the repository
RUN rm -rf /kallithea-repo

# Add static files
RUN mkdir /kallithea
WORKDIR /kallithea
ADD wti_kallithea.ini /kallithea/wti_kallithea.ini

# Upgrade the database
# RUN alembic -c wti_kallithea.ini upgrade head

# Run gearbox
CMD gearbox serve -c wti_kallithea.ini
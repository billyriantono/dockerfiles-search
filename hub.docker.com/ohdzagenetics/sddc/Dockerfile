# Header
FROM biopython/biopython

# Bring source into container
ADD . /src/

# Make sddc alias
# "Install" by setting up aliases
RUN echo 'alias sddc="python /src/sddc.py"' >> ~/.bashrc

# Add short BASH scripts to PATH for non-interactive use
RUN echo '#!/bin/bash sddc' > /usr/bin/sddc && \
        chmod +x /usr/bin/sddc


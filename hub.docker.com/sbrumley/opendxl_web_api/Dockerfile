FROM sbrumley/opendxl:0.1.1

RUN apk add --no-cache bash wget git gcc linux-headers musl-dev

ADD scripts/common.sh scripts/common.sh
ADD scripts/bootstrap.sh scripts/bootstrap.sh
ADD scripts/service.sh scripts/service.sh
ADD scripts/vars.sh scripts/vars.sh
ADD monitor.config monitor.config
ADD templates/ templates/

ADD tests/ tests/

##  MY code
ADD opendxl_web_api.py opendxl_web_api.py

## Install OpenDXL TIE Client
RUN echo "Installing Open DXL TIE Client"
RUN git clone https://github.com/opendxl/opendxl-tie-client-python.git && cd /opendxl-tie-client-python && python setup.py install
RUN apk del git

### Python Common
RUN echo "Installing Python Common"
RUN pip install common

RUN pip install Flask
RUN pip install flask-socketio
RUN pip install eventlet

## Clean UP
RUN apk del --no-cache git gcc linux-headers musl-dev

## Setup Flask Environment
ENV FLASK_APP=/opendxl_web_api.py

CMD /scripts/service.sh debug


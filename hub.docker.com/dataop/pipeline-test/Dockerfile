# docker build --tag dataop/pipeline-test .
# docker run -it dataop/pipeline-test bash

FROM python:3.7-slim
MAINTAINER Dan Bethell <dan@dataop.io>

# Python
RUN pip3 install --upgrade pip
RUN pip3 install virtualenv
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# Go!
CMD ["/bin/bash"]

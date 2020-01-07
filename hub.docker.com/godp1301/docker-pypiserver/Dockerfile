# Copyright (c) 2016 Philippe Godin
#
# See the file LICENSE for copying permission.
FROM ubuntu:14.04
RUN apt-get update && apt-get install -y python-pip
RUN pip install pypiserver
EXPOSE 9000
ENTRYPOINT ["pypi-server", "-p", "9000"]
CMD ["--help"] 

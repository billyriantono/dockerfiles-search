FROM haridasu/scala2.11.7
MAINTAINER Srihari Rao <yolo@srihari.guru>

RUN apt-get update -y && apt-get install -y unzip
RUN curl -O https://downloads.typesafe.com/typesafe-activator/1.3.5/typesafe-activator-1.3.5-minimal.zip
RUN unzip typesafe-activator-1.3.5-minimal.zip -d / && rm typesafe-activator-1.3.5-minimal.zip && chmod a+x /activator-1.3.5-minimal/activator
ENV PATH $PATH:/activator-1.3.5-minimal

EXPOSE 9000 8888
RUN mkdir /app
WORKDIR /app

CMD ["/bin/bash"]
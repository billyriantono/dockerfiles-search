FROM ruby
USER root

RUN gem install s3_website sass && gem cleanup

RUN apt-get update && apt-get install -y openjdk-8-jre-headless unzip zip && apt-get clean

RUN touch /root/.bashrc && curl -s "https://get.sdkman.io" | bash

ADD sdk_wrapper.sh /root/sdk_wrapper.sh
RUN chmod 744 /root/sdk_wrapper.sh

RUN /root/sdk_wrapper.sh install jbake

WORKDIR /site

CMD ["/bin/bash"]

ENTRYPOINT /bin/bash

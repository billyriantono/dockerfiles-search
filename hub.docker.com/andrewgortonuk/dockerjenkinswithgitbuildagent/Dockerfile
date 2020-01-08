FROM maestrodev/build-agent
MAINTAINER Andrew Gorton (http://andrewgorton.uk)

RUN rm -f /var/local/maestro-agent/.m2/settings.xml

ENV HOME /var/local/maestro-agent
ENV RUBYGEMS_API_KEY xxxxx
ENV GEMINABOX https://xxx:yyy@gems.acme.com
ENV PUPPETFORGE_USERNAME john
ENV PUPPETFORGE_PASSWORD doe

CMD su maestro_agent -c '/bin/sh /cmd.sh'

FROM google/nodejs
MAINTAINER Amara "http://amara.org"

RUN apt-get update && apt-get install -y libfreetype6 libfontconfig1
RUN npm install -g karma-cli karma karma-jasmine karma-phantomjs-launcher phantom

CMD ["karma", "start", "--single-run", "--browsers=PhantomJS", "/opt/apps/amara/media/src/js/subtitle-editor/tests/karma.conf.js"]

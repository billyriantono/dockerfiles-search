FROM debian:9.6

RUN apt-get update && apt-get install -y curl gnupg gnupg2 gnupg1
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs gcc g++ make git zip
RUN curl -L https://www.npmjs.com/install.sh | sh
RUN npm install -g @angular/cli -verbose

RUN curl https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.3.0.1492-linux.zip --output sonar-scanner-cli-3.3.0.zip
RUN unzip sonar-scanner-cli-3.3.0.zip && rm -rf sonar-scanner-cli-3.3.0.zip
ENV SONAR_RUNNER_HOME=${WORK_DIR}/sonar-scanner-3.3.0.1492-linux
ENV PATH=${SONAR_RUNNER_HOME}/bin:${PATH}

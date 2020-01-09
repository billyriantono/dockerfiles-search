FROM fedora:23

MAINTAINER mouzil

#RUN dnf -y update
#RUN dnf -y install wget
#RUN dnf -y install tar
#RUN dnf -y install java-1.8.0-openjdk.x86_64
#RUN wget http://apache.mediamirrors.org//jmeter/binaries/apache-jmeter-3.1.tgz
#RUN tar -xvzf apache-jmeter-3.1.tgz
#RUN rm -f apache-jmeter-3.1.tgz
#RUN rm -fr /apache-jmeter-3.1/docs
#RUN mkdir results
#COPY *.jmx ./
#COPY *.csv ./
#VOLUME /apache-jmeter-3.1/bin/results
##CMD ["/apache-jmeter-3.1/bin/jmeter", "-n", "-Jjmeter.save.saveservice.output_format=xml", "-Jjmeter.save.saveservice.assertion_results=all", "-Jjmeter.save.saveservice.response_data=true", "-Jjmeter.save.saveservice.autoflush=true", "-t", "csrf_token_csv_data.jmx", "-l", "/results/tests_results.jtl", "-H", "localhost", "-P", "5000"]
#CMD ["/apache-jmeter-3.1/bin/jmeter", "-n", "-Jjmeter.save.saveservice.output_format=xml", "-Jjmeter.save.saveservice.assertion_results=all", "-Jjmeter.save.saveservice.response_data=true", "-Jjmeter.save.saveservice.autoflush=true", "-t", "csrf_token_csv_data.jmx", "-l", "/results/tests_results.jtl", "-H", "localhost", "-P", "5000"]


RUN dnf -y install git python-pip
RUN python3 -m pip install -U pip
RUN pip3 install flask
RUN pip3 install flask_script
RUN pip3 install flask_bootstrap
RUN pip3 install flask_moment
RUN pip3 install flask_wtf
RUN mkdir -p /home/dev
WORKDIR /home/dev
#RUN git clone https://github.com/mouzil/web_server_flask.git
EXPOSE 5000
WORKDIR /home/dev/web_server_flask
ENTRYPOINT ["python3","hello.py","runserver"]

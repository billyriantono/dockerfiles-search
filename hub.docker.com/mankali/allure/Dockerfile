FROM debian
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN apt-get install -y python-pip
RUN pip install allure-pytest

RUN apt-get -y install default-jre
RUN mkdir /allure
RUN mkdir /allure-report
RUN mkdir /allure-results

ADD ./allure-2.10.0 /allure
RUN chmod +x /allure/bin/allure

ENV PATH="/allure/bin:${PATH}"

EXPOSE 5050
CMD tail -f /dev/null
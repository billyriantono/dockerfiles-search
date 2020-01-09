# Version 0.1

# base
FROM conanio/gcc7

# maintainer
MAINTAINER x-jj@foxmail.com

# operations
# RUN sudo apt-get -yqq update 
# RUN sudo apt-get -yqq upgrade
RUN git clone https://github.com/juj/emsdk.git
RUN cd emsdk && ./emsdk install latest && ./emsdk activate latest
RUN git clone https://github.com/yjjnls/conanos.py.git && cd conanos.py && python setup.py install
# RUN pip install conanos
RUN cd ~/.conan/ && wget https://raw.githubusercontent.com/conanos/dockers/master/emcc/external/0.1.0/settings.yml

CMD ["source", "~/emsdk/emsdk_env.sh"]
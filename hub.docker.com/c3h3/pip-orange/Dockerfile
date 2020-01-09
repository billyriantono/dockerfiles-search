
FROM dockerfile/ubuntu-desktop

RUN apt-get update
RUN apt-get -y install python-numpy libqt4-opengl-dev libqt4-dev cmake qt4-qmake python-sip-dev python-qt4 python-qt4-dev python-qwt5-qt4 python-sip graphviz python-networkx python-imaging python-qt4-gl build-essential python-pip python-scipy python-pyparsing ipython python-matplotlib
RUN easy_install -U distribute

RUN pip install --global-option="build_pyqt_ext" orange



FROM itech/ansible
RUN apt-get -y update \
    && apt-get -y upgrade \
    && apt-get -y install build-essential autoconf libtool pkg-config python-opengl python-imaging python-pyrex python-pyside.qtopengl idle-python2.7 qt4-dev-tools qt4-designer libqtgui4 libqtcore4 libqt4-xml libqt4-test libqt4-script libqt4-network libqt4-dbus python-qt4 python-qt4-gl libgle3 libffi-dev libssl-dev python-dev \
    && easy_install greenlet \
    && easy_install gevent \
    && pip install pytz \
    && pip install shade \
    && apt-get clean 


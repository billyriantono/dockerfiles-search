FROM centos
MAINTAINER suitai <suitai@outlook.jp>
# environment variables
ENV URL https://code.google.com/p/pdsh/
ENV DIR pdsh
# update
RUN yum update -y
RUN yum install -y epel-release
# install
RUN yum install -y git gcc make rpm-build \
                   readline-devel ncurses-devel pam-devel
# git clone
RUN useradd -m rpmbuilder
USER rpmbuilder
WORKDIR /home/rpmbuilder
RUN git clone $URL
# edit spec file
RUN NAME=`perl -na -e '/Name:/ and print $F[1]' $DIR/META` && \
    VERSION=`perl -na -e '/Version:/ and print $F[1]' $DIR/META` && \
    RELEASE=`perl -na -e '/Release:/ and print $F[1]' $DIR/META` && \
    perl -pi -e "s/^Version: /Version: $VERSION/g" $DIR/$NAME.spec && \
    perl -pi -e "s/^Release: /Release: $RELEASE/g" $DIR/$NAME.spec && \
    mv $DIR $NAME-$VERSION && \
    tar zcf $NAME-$VERSION-$RELEASE.tar.gz $NAME-$VERSION
RUN mkdir -p rpmbuild/RPMS/
VOLUME /home/rpmbuilder/rpmbuild/RPMS
CMD rpmbuild -ta $DIR*.tar.gz

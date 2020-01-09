FROM centos:8

ENV SUMMARY="virtio spec" \
    DESCRIPTION="Platform for building virtio specification (centos8)"

LABEL maintainer="Gerd Hoffmann <kraxel@redhat.com>" \
      summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.display-name="${SUMMARY}" \
      io.k8s.description="${DESCRIPTION}" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="virtio" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i"

USER root

RUN dnf install -y liberation-fonts \
                   texlive-amsfonts \
                   texlive-cm \
                   texlive-latex-fonts \
                   texlive-metafont \
                   texlive-metapost \
                   texlive-xetexfontinfo \
                   texlive-zapfding \
		   \
                   texlive-tetex \
                   /usr/bin/htlatex \
                   /usr/bin/pdflatex \
                   /usr/bin/xelatex \
		   \
		   texlive-ae \
		   texlive-babel \
		   texlive-babel-english \
		   texlive-chngcntr \
		   texlive-courier \
		   texlive-ellipsis \
		   texlive-etoolbox \
		   texlive-euenc \
		   texlive-fancyhdr \
		   texlive-fancyvrb \
		   texlive-fontspec \
		   texlive-framed \
		   texlive-geometry \
		   texlive-hyperref \
		   texlive-lastpage \
		   texlive-lineno \
		   texlive-listings \
		   texlive-mdwtools \
		   texlive-multirow \
		   texlive-parskip \
		   texlive-placeins \
		   texlive-rotating \
		   texlive-setspace \
		   texlive-titlesec \
		   texlive-ucs \
		   texlive-underscore \
		   texlive-url \
		   texlive-xcolor \
		   texlive-xifthen \
		   texlive-xltxtra \
		   texlive-xstring \
		   \
                   zip git httpd; \
    dnf clean all -y

COPY ./s2i/bin/ /usr/libexec/s2i
COPY ./etc/virtio-spec-documentroot.conf /etc/httpd/conf.d/
RUN mkdir -p /opt/app-root;\
    chmod 755 /opt /opt/app-root;\
    useradd -d /opt/app-root/src -u 1001 default;\
    mkdir -p /run/httpd;\
    chmod 777 /run/httpd /etc/httpd/logs;\
    sed -i -e '/Listen/s/^/#/' /etc/httpd/conf/httpd.conf;\
    rm -f /etc/httpd/conf.d/welcome.conf

USER 1001
EXPOSE 8080

CMD ["/usr/libexec/s2i/usage"]

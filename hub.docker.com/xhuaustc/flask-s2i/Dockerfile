# springboot-maven3-centos
#
# This image provide a base for running Spring Boot based applications. It
# provides a base Java 8 installation and Maven 3.

FROM centos

EXPOSE 5000

# Change repo to aliyun
COPY ./CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo

COPY ./s2i/bin/ /usr/libexec/s2i

RUN mkdir ~/.pip
COPY pip.conf ~/.pip/pip.conf

RUN yum update -y && \
  yum install -y epel-release && \
  yum install -y python2-pip && \
  pip install --upgrade pip && \
  pip install flask && \
  pip install Flask-SQLAlchemy && \
  pip install PyMySQL && \
  yum clean all


# Add configuration files, bashrc and other tweaks
LABEL io.k8s.description="Flask Webserver" \
    io.k8s.display-name="Flask" \
    io.openshift.expose-services="5000:http" \
    io.openshift.tags="builder,webserver,html,flask" \
    # this label tells s2i where to find its mandatory scripts
    # (run, assemble, save-artifacts)
    io.openshift.s2i.scripts-url="image:///usr/libexec/s2i"

RUN mkdir -p /opt/app
RUN chown -R 1001:0 /opt/app

USER 1001

# Set the default CMD to print the usage of the language image
CMD /usr/libexec/s2i/usage

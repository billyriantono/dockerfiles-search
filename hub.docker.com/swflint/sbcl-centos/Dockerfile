FROM centos
MAINTAINER Sam Flint <swflint@flintfam.org>
# Install sbcl, postgres and libs
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
RUN yum install -y sbcl
RUN yum install -y postgresql-server postgresql-devel postgresql-docs
# Install nginx and multitail
RUN yum install -y nginx multitail
# Install quicklisp, clsql and cl-typesetting
RUN curl -O http://beta.quicklisp.org/quicklisp.lisp
RUN echo '(quicklisp-quickstart:install)' >> quicklisp.lisp
RUN echo '(ql:add-to-init-file)' >> quicklisp.lisp
RUN echo '(ql:quickload "clsql")' >> quicklisp.lisp
RUN echo '(ql:quickload "cl-typesetting")' >> quicklisp.lisp
RUN echo '(quit)' >> quicklisp.lisp
RUN echo > sbcl --load quicklisp.lisp
EXPOSE 22 80
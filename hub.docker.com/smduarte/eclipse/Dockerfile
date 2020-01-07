FROM fedora
RUN useradd me
RUN dnf install -y eclipse-pde git
COPY ./init.sh /
RUN chmod a+x init.sh
CMD [ "/init.sh" ]
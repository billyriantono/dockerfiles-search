FROM centos
COPY google-chrome.repo /etc/yum.repos.d/google-chrome.repo 
RUN yum install -y google-chrome-stable
RUN groupadd -g 998 appuser
RUN useradd -r -u 998 -g appuser appuser
RUN mkdir -p /home/appuser
RUN chown appuser:appuser /home/appuser
USER appuser
CMD ["/usr/bin/google-chrome", "--no-sandbox", "--disable-gpu"]

FROM bitnami/kubectl:1.15.3-debian-9-r117

USER root

RUN wget https://gist.githubusercontent.com/viniciusjssouza/42666e6d01b28ce2deaf1bf426d36929/raw/6d911e7ce9dd8930ce44748538d7277769b43c2f/kexec -O /bin/kexec \
  && chmod +x /bin/kexec \
  && wget https://gist.githubusercontent.com/viniciusjssouza/4e0bc176cde2df8d75a94647fca46d7d/raw/ee7396277e22c65c172740c21032d65017e60d0f/klogs -O /bin/klogs \
  && chmod +x /bin/klogs \
  && wget https://gist.githubusercontent.com/vitebo/7e5e02b78c0416720c74935fedd4f930/raw/ac7074ccccb3273d8d7e6b17a2386efcc877241a/kube-prompt.sh -O /root/kube-prompt.sh \
  && chmod +x /root/kube-prompt.sh \
  && wget https://gist.githubusercontent.com/vitebo/7e5e02b78c0416720c74935fedd4f930/raw/ac7074ccccb3273d8d7e6b17a2386efcc877241a/.bashrc -O /root/.bashrc \
  && chmod +x /root/.bashrc

ENTRYPOINT "/bin/bash"

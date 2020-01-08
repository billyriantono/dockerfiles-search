FROM kr3ssh/debian-rbenv
MAINTAINER Sergey Besedin "kr3ssh@gmail.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y ssh nodejs sudo nginx npm mongodb-clients postgresql-client redis-tools vim

# Dirty fix after stupid nodejs developers
RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN mkdir /var/run/sshd

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN sed -ri 's/AcceptEnv LANG LC_\*/# AcceptEnv LANG LC_\*/g' /etc/ssh/sshd_config

RUN echo 'root:root' | chpasswd

RUN useradd -m -s /bin/bash rack

# Configure SSH access
RUN mkdir -p /home/rack/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDMsNyQdz05or5o3jovzjlemvv8sImk649iicUIpy3g2HDgFRRioMOq6FaXDMYZKOgdZNHfe3Fm9a2P+SpJdhb+3zqrZZ3mPBSYOmYyZKwwoDHlUsgq90IIKBX2mvfS1oOm+xOOE3NcWjkTZ+r6RgaWt8iKIwnW0RkPmVLlc1MIKlp/vcPyo5HpshXT89+sJyavXhoEhGacn58elbjkjnlAkjt5tCalstmOTT8f9RqjLDkwNkIHx/STCKngs2FO5Fr8AcR5kLt/PMgjTQ+W5bMk0FZnVSnDv9mGwinRnTRQE8K30sU+6AgZ8C+pOYDdedOqkvlOXu6A4uc7uKR103kN rack@docker-rails" > /home/rack/.ssh/authorized_keys

#-----BEGIN RSA PRIVATE KEY-----
#MIIEowIBAAKCAQEAzLDckHc9OaK+aN46L845Xpr7/LCJpOuPYonFCKct4Nhw4BUU
#YqDDquhWlwzGGSjoHWTR33txZvWtj/kqSXYW/t86q2Wd5jwUmDpmMmSsMKAx5VLI
#KvdCCCgV9pr30taDpvsTjhNzXFo5E2fq+kYGlrfIiiMJ1tEZD5lS5XNTCCpaf73D
#8qOR6bIV0/PfrCcmr14aBIRmnJ+fHpW45I55QJI7ebQmpbLZjk0/H/Uaoyw5MDZC
#B8f0kwip4LNhTuRa/AHEeZC7fzzII00PluWzJNBWZ1Upw7/ZhsIp0Z00UBPCt9LF
#PugIGfAvqTmA3XnTqpL5Tl7ugOLnO7ikddN5DQIDAQABAoIBAQC9u8L3dk+eOShe
#dH9jCLlM5ERnegxcfq0uHZ4x4yU3oekfDOsUcQhuR2bcJM8LS0u801Nm4DnBwkDb
#j46PAZNXNPxhG5Q9cbt1T8yjMYYanKMjepRon0Dp5p5VNFg7avQlt93seEMae9ck
#EdNRoc9BraGJyei44qFkQC8C2N9CVLeWY3+kmcOj1DAWA4OFAVmm+gpAMOdhWJXe
#1QLrEF970qb4SDwofCp2LuLWIEL4PCIbYx6CqAMDH6PJmd8Xp18DMpRa5DzOLMeg
#+kyBmRIVHuCE/8tcvTu+wld4aqJodD34ct83OC8jZHM34JZ3SO+Bfe3CIQdRiQrw
#xnrmI3tRAoGBAOjU1ZlFz34OHpFeidvanN0lxSO6GBHV2qgU/Ut7EauvlftSq647
#8CUjofW8gdRRZfdYP38sSXQTYFSbsp3YAcqPUU+NVPANTudCyuL1jRlzdrfqmx5I
#pwl1EveDGHdiuOF0SlaYThzjU0OHetPH4+7dMn9U9NV+a4V3sBb2HCEDAoGBAOEP
#LGBhK6Eb0TIfQxqFpgFJ/8gcfiIp5xpNxJWHv3oGTDkYFa8cCKWbVAQjOxIHRbuz
#kMVt0KMB8oGhdDpQNK2KtDwGnI1rcxrSgmvCJGn2dTB/udL+DYAAKWFKg7+YJqXx
#WpV6uetd6EKSGChSqMLkwDUzDVA0NVpXWnoPivivAoGAX415W73audDxmpdB3IiL
#d/bYQSFOX4N0iSaUDTYkumEFHG+BJbBTjephvYfvgEMnpasB5B84xfptvktnsn/D
#vG204QEPqrTLfP1cZmh/z8IjJreRkYwfgTIa5plWoShS17PyDjfTVue0dDJVpjSS
#xqTg5IDpOfT4C35jNgkq4iECgYAKIkvGPznetEj0L9IutIvoDPP2h8nqMebVGWFb
#tlQZ44S1IW+AhguhoV/kG84CHs+2Bvzi1vIJFQJdce6w3YGxusgo18de2tLBB2+V
#+JT5LH7UYzvz0zq6Y8d5OQi7rNc4q6h/iJosjfryXG+4CRjORcyd2KGl1eP9IGfT
#jTWdwwKBgH3z9MMKbz9Hdi4FKMwtBr7iXrgqKtfCI4HIbd0bTHhdotE2a5fWxilW
#WoZvBVQxUY//oXZ98jk/YodPLLeq8l/BgEtU6ggtF1RMie+ovSqxLx+gvaUBapAc
#LqP4uSVmktuP/iZwBn9vlRkKiJo0chPNqYfzuknAcgeYgpT2zHDB
#-----END RSA PRIVATE KEY-----

RUN chown -R rack: /home/rack
RUN echo -n 'rack:rack' | chpasswd

# Enable passwordless sudo for rack
RUN mkdir -p /etc/sudoers.d && echo "rack ALL= NOPASSWD: ALL" > /etc/sudoers.d/rack && chmod 0440 /etc/sudoers.d/rack

USER rack

RUN echo 'export RAILS_ENV=development' >> /home/rack/.profile
RUN echo '\n\
alias rails="bundle exec rails"\n\
alias rake="bundle exec rake"\n\
alias rspec="bundle exec rspec"\n\
alias cap="bundle exec cap"\n\
' >> /home/rack/.bashrc

RUN rbenv install 1.9.3-p448
RUN rbenv install 2.1.3
RUN rbenv install 2.1.5
RUN rbenv install 2.2.0

USER root

RUN /etc/init.d/nginx stop

RUN apt-get clean

EXPOSE 80 22

# Dockerize ssh daemon. All further jobs will run through ssh session
CMD nginx && /usr/sbin/sshd -D

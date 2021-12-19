FROM ubuntu:16.04

RUN apt-get update

RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

ARG ROOT_PASSWORD=root
ARG SSH_PORT=2222

RUN echo 'root:${ROOT_PASSWORD}' |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#\s+?Port 22/Port ${SSH_PORT}}/g' /etc/ssh/sshd_config

RUN mkdir /root/.ssh

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]

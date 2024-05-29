# Ubuntu 20.04 with sshd enabled
# andy30sh/ubuntu:20.04

# docker build -t andy30sh/ubuntu-sftp:20.04 . --no-cache
# docker run -d -it --name [ContainerName] -p 22:22 --hostname [ContainerHostname] andy30sh/ubuntu-sftp:20.04
# -v [HostPath]:/shared -v [HostPath]:/storage

FROM ubuntu:20.04

RUN apt-get update
RUN apt-get install -y openssh-server openssh-client
RUN apt-get install -y sudo
RUN apt-get install -y nano
RUN apt-get install -y vim
RUN apt-get install -y wget
RUN apt-get install -y net-tools

RUN mkdir -p /root/.ssh
RUN touch /root/.ssh/authorized_keys
RUN chmod 700 -R /root/.ssh
RUN cd /root/.ssh/
ADD vm.pub /root/.ssh/
ADD vm.ppk /root/.ssh/
RUN cat /root/.ssh/vm.pub >> /root/.ssh/authorized_keys
RUN rm -f /root/.ssh/vm.pub

RUN mkdir -p /var/run/sshd
RUN echo 'root:passwd' | chpasswd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

VOLUME [ "/shared", "/ftp_data" ]

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

# /share/CACHEDEV1_DATA/FTP_Data
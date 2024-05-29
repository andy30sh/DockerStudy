# Ubuntu 20.04 with sshd enabled
# andy30sh/ubuntu:22.04

# docker build -t andy30sh/webapp:22.04 -t andy30sh/webapp:latest --no-cache
# docker image push --all-tags andy30sh/webapp

# docker run -d -it --name [ContainerName] -p 22:22 --hostname [ContainerHostname] andy30sh/ubuntu:22.04
# -v [HostPath]:/shared -v [HostPath]:/storage

FROM ubuntu:22.04

RUN apt-get update
RUN apt-get install -y openssh-server openssh-client
RUN apt-get install -y sudo
RUN apt-get install -y nano
RUN apt-get install -y vim
RUN apt-get install -y wget
RUN apt-get install -y net-tools

# For program development packages
RUN apt-get install -y git
RUN apt-get install -y subversion
RUN apt-get install -y build-essential
RUN apt-get install -y python3 python3-pip
RUN ln -s /usr/bin/python3 /usr/bin/python
RUN apt-get install -y default-jdk
RUN apt-get install -y mysql-client
RUN apt-get install -y mongodb-org
RUN apt-get install -y curl dirmngr apt-transport-https lsb-release ca-certificates
#RUN curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
RUN apt-get install -y nodejs npm
RUN npm install -g express
RUN npm install -g nodemon

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

VOLUME [ "/web", "/data", "/shared" ]

EXPOSE 22/tcp 3000 27017
CMD ["/usr/sbin/sshd", "-D"]
FROM ubuntu:trusty
MAINTAINER Peter Pouliot "peter@pouliot.net"

RUN wget http://apt.puppetlabs.com/puppetlabs-release-trusty.deb; dpkg -i puppetlabs-release-trusty.deb
RUN apt-get update -y
RUN apt-get install -y git screen ipmitool openipmi openssh-server openjdk-7-jre puppet ruby ruby-dev
RUN gem install r10k
RUN gem install hiera-eyaml
RUN echo "root:ubuntu" | chpasswd
RUN useradd jenkins
RUN echo "jenkins:jenkins" | chpasswd
RUN mkdir /var/run/sshd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ADD id_dsa /root/.ssh/id_dsa
ADD id_dsa.pub /root/.ssh/id_dsa.pub
ADD authorized_keys2 /root/.ssh/authorized_keys2
EXPOSE 22
CMD["/usr/sbin/sshd", "-D"]

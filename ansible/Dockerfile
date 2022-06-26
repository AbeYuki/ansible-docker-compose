FROM ubuntu:20.04
RUN apt-get update && apt-get install -y \
    software-properties-common \
    ca-certificates \
    curl \
    gnupg \
    wget \
    sudo \
    && apt-add-repository --yes --update ppa:ansible/ansible \
    && apt-get install -y ansible
RUN mkdir /root/.ssh/ 
RUN ssh-keygen -f /root/.ssh/id_ecdsa -t ecdsa -b 521 -N '' \
    && cp -p /root/.ssh/id_ecdsa.pub /root/.ssh/authorized_keys
ADD ansible.cfg /etc/ansible
CMD ["/bin/bash"]
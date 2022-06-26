FROM ubuntu:20.04
RUN apt-get update && apt-get install -y \
    software-properties-common \
    ca-certificates \
    curl \
    gnupg \
    openssh-server \
    sudo \
    wget 
RUN echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config \
    && echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config \
    && echo 'AuthorizedKeysFile /root/.ssh/authorized_keys' >> /etc/ssh/sshd_config \
    && echo 'PubkeyAuthentication yes' >> /etc/ssh/sshd_config \
    && mkdir /root/.ssh/ \
    && touch /root/.ssh/authorized_keys
RUN echo "root:node" | chpasswd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
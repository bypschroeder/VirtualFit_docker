FROM linuxserver/blender:4.3.1

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-dev \
    python3-pip \
    git \
    wget \
    openssh-server && \
    mkdir /var/run/sshd && \
    apt-get clean

WORKDIR /vf_blender
RUN git clone https://github.com/bypschroeder/VirtualFit_blender.git .

RUN echo "root:root" | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
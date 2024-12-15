FROM python:3.11.0-slim

WORKDIR /api

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    openssh-server && \
    mkdir /var/run/sshd && \
    apt-get clean

RUN git clone https://github.com/bypschroeder/VirtualFit_api.git .
RUN pip install -r requirements.txt

RUN echo "root:root" | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

EXPOSE 22 3000

RUN echo "#!/bin/bash\n" \
    "service ssh start\n" \
    "python ./main.py\n" > /api/start.sh && \
    chmod +x /api/start.sh

CMD ["/api/start.sh"]
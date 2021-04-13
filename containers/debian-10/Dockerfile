FROM debian:10

# Zuul minimal package
RUN apt-get update && \
    apt-get install -y \
        black \
        git \
        iproute2 \
        python3-apt \
        python3-flake8 \
        python3-pip \
        python3-setuptools \
        python3-virtualenv \
        rsync \
        sudo \
        traceroute \
        wget \
        yamllint

# Zuul uses revoke-sudo. We can simulate that by moving the default sudoers to zuul
# And this will prevent root from using sudo when the file is removed by revoke-sudo
RUN mv /etc/sudoers /etc/sudoers.d/zuul && grep includedir /etc/sudoers.d/zuul > /etc/sudoers && sed -e 's/.*includedir.*//' -i /etc/sudoers.d/zuul && chmod 440 /etc/sudoers

# Create fake zuul users
RUN echo "zuul:x:0:0:root:/root:/bin/bash" >> /etc/passwd

# Enable root local bin
ENV PATH=/root/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
WORKDIR /root

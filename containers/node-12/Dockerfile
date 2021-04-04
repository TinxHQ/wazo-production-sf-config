FROM node:12-buster

# Zuul minimal package
RUN apt-get update && \
    apt-get install -y sudo rsync git traceroute iproute2 python3-setuptools python3-pip && \
    pip3 install flake8 yamllint

# Zuul uses revoke-sudo. We can simulate that by moving the default sudoers to zuul
# And this will prevent root from using sudo when the file is removed by revoke-sudo
RUN mv /etc/sudoers /etc/sudoers.d/zuul && grep includedir /etc/sudoers.d/zuul > /etc/sudoers && sed -e 's/.*includedir.*//' -i /etc/sudoers.d/zuul && chmod 440 /etc/sudoers

# Create fake zuul users
RUN echo "zuul:x:0:0:root:/root:/bin/bash" >> /etc/passwd

# Enable root local bin
ENV PATH=/root/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
WORKDIR /root

FROM python:3.10-slim-bullseye

# Zuul minimal package
RUN apt-get update && \
    apt-get install -y  \
      # base packages for Zuul
      sudo \
      rsync \
      git \
      traceroute \
      iproute2 \
      # Required for bindep in tox ansible job
      python3-apt \
      python3-setuptools

# Zuul uses revoke-sudo. We can simulate that by moving the default sudoers to zuul
# And this will prevent root from using sudo when the file is removed by revoke-sudo
RUN mv /etc/sudoers /etc/sudoers.d/zuul && grep includedir /etc/sudoers.d/zuul > /etc/sudoers && sed -e 's/.*includedir.*//' -i /etc/sudoers.d/zuul && chmod 440 /etc/sudoers

# Create fake zuul users
RUN echo "zuul:x:0:0:root:/root:/bin/bash" >> /etc/passwd

# Enable root local bin
ENV PATH=/root/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
WORKDIR /root

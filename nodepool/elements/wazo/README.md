# Wazo base

Install Wazo basic requirements, plus docker.

Add a `wazo-debug` user

- Any Wazo developper can SSH in, relying on keys in https://github.com/wazo-platform/wazo-dev-ssh-pubkeys
- The user can becomes root through `sudo -i`
- There's a password specified to be able to log in through TTY if there's a network issue

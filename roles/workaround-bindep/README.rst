Workaround for bindep

Issue: bindep role use generic module 'package' to install system package. no `apt update` will be
triggered and since this role is run at the beggining on new VM, the cache is empty

Note: Previous roles (i.e. ensure-pip) may hide the issue, because `apt update` is triggered

Limitations: All roles must now run on a debian based image

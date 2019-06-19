# ansible-pull-configure

## Overview
This role will create a working directory for cloning the ansible repo containing all host configuration, in this case it is [https://github.com/broadinstitute/DSP-ansible-configs]. Along with configuring a cron job to have 15 minute reoccurring checkins with the repo looking for changes. It also creates a log rotation for all the ansible logs and kicks off an initial checkin so you will not have to wait 15 minutes.

#### Assumptions
- python is installed in a virtual environment and a cron job cannot source its path so the cron job is a fully qualified path `/usr/local/bin/ansible/bin/ansible-pull`.
- `<role-name>/meta/main.yml` is needed if using ansible-galaxy in the [ansible-role-clone-repos](https://github.com/broadinstitute/DSP-ansible-configs/tree/master/roles/ansible-role-clone-repos)

### Instance Labels
ANSIBLE_REPO: git repo where main ansible configs are stored.  Defaults to "https://github.com/broadinstitute/dsp-ansible-configs.git"
ANSIBLE_PROJECT: this is the ansible playbook name that the instance should use.  Defaults to the Google Project name
ANSIBLE_BRANCH: git branch to use in the gitrepo for this instance.  Defaults to "master"

#### Defaults
```
# schedule is fed directly to cron
schedule: '*/15 * * * *'

# User to run ansible-pull as from cron
cron_user: root

# File that ansible will use for logs
logfile: /var/log/ansible-pull.log

# Directory to where repository will be cloned
workdir: /var/lib/ansible/local

#set proper inverntory PATH
inventory: "/var/lib/ansible/local/inventories/{{ gproject }}/hosts"

```

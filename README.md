# ansible-pull-configure

## Overview
This role will create a working directory for cloning the ansible repo containing all host configuration, in this case it is [https://github.com/broadinstitute/DSP-ansible-configs]. Along with configuring a cron job to have 15 minute reoccurring checkins with the repo looking for changes. It also creates a log rotation for all the ansible logs and kicks off an initial checkin so you will not have to wait 15 minutes.

#### Assumptions
- pyhton is installed in a virtual environment and a cron job cannot source its path so the cron job is a fully qualified path `/usr/local/bin/ansible/bin/ansible-pull`.
- `<role-name>/meta/main.yml` is needed if using ansible-galaxy in the [ansible-role-clone-repos](https://github.com/broadinstitute/DSP-ansible-configs/tree/master/roles/ansible-role-clone-repos)

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

# Repository to check out -- YOU MUST CHANGE THIS
# repo must contain a local.yml file at top level
#repo_url: git://github.com/sfromm/ansible-playbooks.git
repo_url: https://github.com/broadinstitute/DSP-ansible-configs.git

#pull google project var
gproject: "{{ lookup('env','GPROJECT') }}"

#set proper inverntory PATH
inventory: "/var/lib/ansible/local/inventories/{{ gproject }}/hosts"

#playbook to run
playbook: "{{ gproject }}.yml"
```

Role Name
=========

Installs and configures apt-mirror (Local APT Repository). Also configures clients if extra-var passed.

Requirements
------------

Install Ansible role requirements
````
sudo ansible-galaxy install -r requirements.yml -f
````

Vagrant
-------
Spin up Environment under Vagrant to test.
````
vagrant up
````

Docker
------
Spin up Docker container (apt mirror repos not populated...will update on cron schedule)
````
docker run -d -p 80:80 mrlesmithjr/apt-mirror
````

Role Variables
--------------
````
---
# defaults file for ansible-apt-mirror
apache2_default_root: /var/www/html
apt_mirror_apache_links:  #defines the uri of each repository used in apt_mirror_repos..ex. http://archive.ubuntu.com/ubuntu will be archive.ubuntu.com/ubuntu
  - uri: archive.ubuntu.com/ubuntu/
    distro: ubuntu  #defines name of symlink..ensure to change apt_mirror_client_repos to match
apt_mirror_client: false  #defines if running this role against a client...define this as an extra-var...example in README.md
apt_mirror_client_repos:
  - 'deb http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }} main restricted universe multiverse'
  - 'deb http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-security main restricted universe multiverse'
  - 'deb http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-updates main restricted universe multiverse'
#  - 'deb http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-proposed main restricted universe multiverse'
#  - 'deb http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-backports main restricted universe multiverse'
  - 'deb-src http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }} main restricted universe multiverse'
  - 'deb-src http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-security main restricted universe multiverse'
  - 'deb-src http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-updates main restricted universe multiverse'
#  - 'deb-src http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-proposed main restricted universe multiverse'
#  - 'deb-src http://{{ apt_mirror_repo_server }}/ubuntu {{ ansible_distribution_release }}-backports main restricted universe multiverse'
apt_mirror_dir: /myrepo  #define directory to use as repo
apt_mirror_nthreads: 20  #defines the number of threads
apt_mirror_populate_repos: true  #defines if repos should be populated during install..can set to false and allow cron job to populate.
apt_mirror_repos:  #define list of repos to add
## Ubuntu Trusty (14.04)
  - 'deb http://archive.ubuntu.com/ubuntu trusty main restricted universe multiverse'
  - 'deb http://archive.ubuntu.com/ubuntu trusty-security main restricted universe multiverse'
  - 'deb http://archive.ubuntu.com/ubuntu trusty-updates main restricted universe multiverse'
#  - 'deb http://archive.ubuntu.com/ubuntu trusty-proposed main restricted universe multiverse'
#  - 'deb http://archive.ubuntu.com/ubuntu trusty-backports main restricted universe multiverse'
  - 'deb-src http://archive.ubuntu.com/ubuntu trusty main restricted universe multiverse'
  - 'deb-src http://archive.ubuntu.com/ubuntu trusty-security main restricted universe multiverse'
  - 'deb-src http://archive.ubuntu.com/ubuntu trusty-updates main restricted universe multiverse'
#  - 'deb-src http://archive.ubuntu.com/ubuntu trusty-proposed main restricted universe multiverse'
#  - 'deb-src http://archive.ubuntu.com/ubuntu trusty-backports main restricted universe multiverse'
## Ubuntu Precise (12.04)
#  - 'deb http://archive.ubuntu.com/ubuntu precise main restricted universe multiverse'
#  - 'deb http://archive.ubuntu.com/ubuntu precise-security main restricted universe multiverse'
#  - 'deb http://archive.ubuntu.com/ubuntu precise-updates main restricted universe multiverse'
apt_mirror_schedule:
  - name: 'apt-mirror updates'
    special_time: daily  #defines easy schedule....can be hourly, daily, weekly, monthly, annually, yearly or reboot..comment out if setting specific times
#    minute: 0
#    hour: *
#    day: *
#    month: *
#    weekday: *
    job: '/usr/bin/apt-mirror > /var/spool/apt-mirror/var/cron.log'
    cron_file: apt-mirror
apt_mirror_schedule_updates: true  #defines if repos should be updates on a schedule...defined in apt_mirror_schedule
apt_mirror_repo_server: 'apt-mirror.{{ pri_domain_name }}'  #defines server clients point to...either FQDN/hostname/IP
apt_mirror_reset_client: false  #defines if clients sources.list should be reset to default
pri_domain_name: example.org
````

Dependencies
------------

ansible-apache2 and mrlesmithjr.apache2 (Installed as part of requirements.yml)

Example Playbook
----------------

###### Galaxy
    - hosts: servers
      roles:
         - role: mrlesmithjr.apache2
         - role: mrlesmithjr.apt-mirror

     - hosts: clients
       roles:
         - { role: mrlesmithjr.apt-mirror, apt_mirror_client: true }

###### GitHub
    - hosts: servers
      roles:
        - role: ansible-apache2
        - role: ansible-apt-mirror

    - hosts: clients
      roles:
        - { role: ansible-apt-mirror, apt_mirror_client: true }

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com

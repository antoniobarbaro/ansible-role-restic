Role Name
=========

Install Restic backups tool

Requirements
------------

None

Role Variables
--------------

General variable
restic_download_url: Restic executable download url. Default: 'https://github.com/restic/restic/releases/download/v0.7.1/restic_0.7.1_linux_amd64.bz2'
restic_repository_path: Backup repository path. Default. '/var/backup'
restic_password: Backup repository password: Default: 'Entrata@01'

Cron variable
restic_cron_enable: Enable restic cron script. Default: no 
restic_cron_minute: Restic cron minute. Default:'*'  
restic_cron_hour: Restic cron hour. Default:'*'
restic_cron_day: Restic cron day. Default:'*'
restic_cron_month: Restic cron month. Default:'*'
restic_cron_weekday: Restic cron weekday. Default:'*'
restic_backup_items: List of baskup Items. Default list:
  - "restic backup /var/ossec --tag ossec"
  - "restic forget --tag ossec --keep-daily 7 --keep-weekly 5 --keep-monthly 7 --prune"

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      vars:
        restic_cron_minute: '*/3'
        restic_cron_enable: yes     
      restic_backup_items:
        - "restic backup /var/log --tag log"        
        - "restic backup /etc --tag etc" 
        - "mysqldump [...] | restic -r backup --stdin --tag mysql"
      roles:
         - restic

License
-------

BSD

Author Information
------------------

Antonio Barbaro <antonio.barbaro@gmail.com>

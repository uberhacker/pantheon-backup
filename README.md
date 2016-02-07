###Bash shell script to backup all Pantheon sites and environments

###Purpose:
  Backs up all or individual elements for all or individual environments of all available Pantheon sites.

###Installation:

```
  $ git clone https://github.com/uberhacker/pantheon-backup.git
  $ cd pantheon-backup
  $ chmod +x pantheon-backup
  $ sudo cp pantheon-backup /usr/local/bin
```

###Usage:

```
  $ pantheon-backup [dev|test|live|all] [code|database|files|all]
```

  *The first argument is the environment and defaults to all.*

  *The second argument is the element and defaults to all.*

###Examples:
  *pantheon-backup*

    Backup all elements in all environments of all available sites

  *pantheon-backup dev*

    Backup all elements in the dev environment only of all available sites

  *pantheon-backup all code*

    Backup the code only for all environments of all available sites

  *pantheon-backup live database*

    Backup the database only for the live environment only of all available sites

  *pantheon-backup live all*

    Backup all elements of the live environment only for all available sites

###Example crontab entry:

```
# Backup all Pantheon sites daily at 3 AM.
0 3 * * * /usr/local/bin/pantheon-backup 2>&1 >> /var/log/pantheon-backup.log
```

###Troubleshooting:

  If you get an error during backup similar to the following:
  ```
  [Error] Backup skipped for dev environment of my-pantheon-site because the environment has not been created.
  ```
  and you know the site has been created and set to git connection mode, try switching from git to sftp mode and then back to git mode.
  Then try the backup again.

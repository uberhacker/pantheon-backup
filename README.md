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
  $ pantheon-backup [dev|test|live|all] [code|database|files|all] [commit|skip|ignore]
```

  *The first argument is the environment and defaults to all.*

```
  dev - Development environment

  test - Staging environment

  live - Production environment

  all - All environments including any multi-site environments
```

  *The second argument is the element and defaults to all.*

```
  code - Code element (files inside the git repository)

  database - Database element (MariaDB dump)

  files - Files element (files outside the git repository)

  all - Code, database and files elements
```

  *The third argument decides how to handle pending filesystem changes and defaults to commit.*

```
  This argument is only necessary when the environment is in sftp connection mode.

  commit - Commit pending filesystem changes before performing the backup

  skip - Skip the backup entirely if filesystem changes are pending

  ignore - Perform the backup without committing pending filesystem changes
```

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

  *pantheon-backup dev code ignore*

    Backup the code only of the dev environment only for all available sites
    and perform the backup without committing pending filesystem changes

###Example crontab entry:

```
# Backup all Pantheon sites daily at 3 AM.
0 3 * * * /usr/local/bin/pantheon-backup 2>&1 >> /var/log/pantheon-backup.log
```

###Troubleshooting:

  If you get an error during backup similar to the following:
  ```
  ... [Error] Backup skipped for XXX in YYY environment of ZZZ site because the environment has not been created.
  ```
  and you know the site has been created and set to git connection mode, try switching from git to sftp mode and then back to git mode.
  Then try the backup again.

# Rin's s6 management tool

A tool I wrote to make using s6 and s6-rc easier (especially for user installations).
If you're not familiar with how s6 and s6-rc work, then I'd recommend not
using this tool in case problems occur.

# Usage

```
./rs6 [switches | options] command [command_args...]

  commands:
    init s6                          Run s6-svscan
    init s6-rc                       Initialize s6-rc live state
    compile_db SERVICE_DEF_DIR...    Compile a s6-rc database from definitions
    switch_live_db NEW_DB            Switch which database an s6-rc instance is using
    change_default_db NEW_DB         Change which database is used for initialization
    upgrade_db SERVICE_DEF_DIR...    Compile db, switch and change default
    sv list up                       List active services
    sv list down                     List inactive services
    sv start SERVICE                 Start a service
    sv stop SERVICE                  Stop a service
    sv restart SERVICE               Restart a service
    rc AGRS...                       Run s6-rc with provided args
    env add VAR VALUE                Add variable to envdir
    env del VAR                      Remove variable from envdir
    env list                         List virables defined in envdir
    env get VAR                      Print value of variable from envdir

  switches:
    -n        Dry run (print commands instead of executing them)

  options:
    -d  DB_DIR:         s6-rc database directory
          init s6-rc
          compile_db
          change_default_db
          upgrade_db

    -e  ENV_DIR:        s6-envdir environment directory
          init s6
          env

    -l  LIVE_DIR:       s6-rc live state directory
          init s6-rc
          switch_live_db
          upgrade_db
          sv list
          sv start
          sv stop
          rc
        LOG_FILE:       file to save s6-svscan logs to
          init s6

    -s  SERVICE_DIR:    s6-svscan service directory
          init s6
          init s6-rc
          sv restart
```

# Design choices

## Why is s6-svscan running in abduco?

This tool was made primarily for me to administer per-user s6 + s6-rc trees.
Using abduco for the svscan process allows the daemons to persist even when the
user logs out.

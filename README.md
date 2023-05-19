# Rin's s6-rc management tool (WIP)

A tool I wrote to make using s6 and s6-rc easier.
If you're not familiar with how s6 and s6-rc work, then I'd recommend avoiding
using this tool in case problems occur.

# Usage

```
rs6 [options] command

  options:
    -n                dry run

  commands:
    init_s6           Runs s6-svscan in abduco
    init_s6-rc        Initializes s6-rc state
    compile_db        Compiles a new db from the service definitions
    update_live_db    Updates the db that s6-rc is using to the newest one

```

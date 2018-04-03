# Scipts for m
Here are some scripts and best practices for quickly creating MongoDB clusters using [m](https://github.com/aheckmann/m) along with [mlaunch](https://github.com/rueckstiess/mtools/wiki/mlaunch) from mtools.

Each cluster is created in its own directory, following the convention `Version_Replica Set_Shards`. For example:

    362_pss_sh4

Start by copying an existing directory to the new directory, following the naming convention of the type of cluster you want to create. Then delete the `data` directory that was copied over, as this will be re-created.

Customize your cluster by changing the following files:
- VERSION 
- PORT 

    Recommendation is to use version00 to avoid conflicts, e.g., 36200

- init

    Customize the [mlaunch](https://github.com/rueckstiess/mtools/wiki/mlaunch) script to create the desired cluster. 


Then:
- create and start a cluster with `./init`
- stop a cluster with `mlaunch stop`
- restart a cluster with `./start`
- reinitiate a cluster by first removing the `data` directory (ensure all mongo processes are dead too)
- start a mongo shell to the primary port of the cluster with `./mongo`

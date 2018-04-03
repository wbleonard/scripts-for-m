# Scipts for m
Here are some scripts and best practices for quickly creating MongoDB clusters using [m](https://github.com/aheckmann/m) along with [mlaunch](https://github.com/rueckstiess/mtools/wiki/mlaunch) from [mtools](https://github.com/rueckstiess/mtools/blob/develop/README.rst).

These scripts were created by [Daniel Coupal](https://github.com/dcoupal) and he's agreed to allow me to post them here.

## Overview
Via a couple of configuration files and an initialization script, it's very easy to initialize, start and stop MongoDB clusters of varying versions and configurations. The process involves copying an existing configuration, adjusting the parameters to match your desired configuration, and initializing the cluster.

## Prerequisites
[m](https://github.com/aheckmann/m) and [mtools](https://github.com/rueckstiess/mtools/blob/develop/README.rst) are installed.

## Configuring a New Cluster

Clone this repository

    git clone https://github.com/wbleonard/scripts-for-m.git


Each cluster is created in its own directory, following the convention `Version_RepSetConfig_Shards`. For example:

    362_pss_sh4

Start by copying an existing directory to the new directory, following the naming convention of the type of cluster you want to create: 

    cp -r 362_pss_sh4/ 363_pss_sh5

Then delete the `data` directory that was copied over, as this will be re-created:

    rm -r 363_pss_sh5/data/

Install the version of MongoDB you wish to use:

    m 3.6.3

Customize your cluster by changing the following files:
- VERSION 
- PORT 

    The recommendation is to use <version>00 to avoid port conflicts, e.g., 36200

- init

    Customize the [mlaunch](https://github.com/rueckstiess/mtools/wiki/mlaunch) script to create the desired cluster. 


## Using

- create and start a cluster with `./init`
- stop a cluster with `mlaunch stop`
- restart a cluster with `./start`
- reinitiate a cluster by first removing the `data` directory (ensure all mongo processes are dead too)
- start a mongo shell to the primary port of the cluster with `./mongo`

## Helpful Tips

 - Use `m --stable` to find the latest stable release of MongoDB
- Use `m <version>` to install the version
- Use `m bin <version>` to verify you have the correct version installed.

## Troubleshooting

If `./init` fails, verify you have the correct version of MongoDB installed (`m bin <version>`)

    ./init
    Traceback (most recent call last):
    File "/usr/local/bin/mlaunch", line 11, in <module>
        sys.exit(main())
    ...
    OSError: [Errno 2] No such file or directory
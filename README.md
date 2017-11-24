Ansible Container for JIRA
==========================

[![Travis](https://img.shields.io/travis/alvistack/ansible-container-jira.svg)](https://travis-ci.org/alvistack/ansible-container-jira)
[![GitHub release](https://img.shields.io/github/release/alvistack/ansible-container-jira.svg)](https://github.com/alvistack/ansible-container-jira/releases)
[![GitHub license](https://img.shields.io/github/license/alvistack/ansible-container-jira.svg)](https://github.com/alvistack/ansible-container-jira/blob/master/LICENSE)
[![Ansible Role](https://img.shields.io/badge/galaxy-alvistack.container--jira-blue.svg)](https://galaxy.ansible.com/alvistack/container-jira)
[![Docker Pulls](https://img.shields.io/docker/pulls/alvistack/ansible-container-jira.svg)](https://hub.docker.com/r/alvistack/ansible-container-jira/)

Ansible Container for Atlassian JIRA.

JIRA Software unlocks the power of agile by giving your team the tools to easily create & estimate stories, build a sprint backlog, identify team commitments & velocity, visualize team activity, and report on your team's progress.

Learn more about JIRA: <https://www.atlassian.com/software/jira>

Overview
--------

This Docker container makes it easy to get an instance of JIRA up and running.

### Quick Start

For the `JIRA_HOME` directory that is used to store the repository data (amongst other things) we recommend mounting a host directory as a [data volume](https://docs.docker.com/engine/tutorials/dockervolumes/#/data-volumes), or via a named volume if using a docker version &gt;= 1.9.

Volume permission is managed by entry scripts. To get started you can use a data volume, or named volumes.

Start Atlassian JIRA Server:

    docker run \
        -itd \
        -n jira \
        -p 8080:8080 \
        -v /var/atlassian/application-data/jira:/var/atlassian/application-data/jira \
        alvistack/ansible-container-jira

**Success**. JIRA is now available on <http://localhost:8080>

Please ensure your container has the necessary resources allocated to it. We recommend 2GiB of memory allocated to accommodate both the application server and the git processes. See [Supported Platforms](https://confluence.atlassian.com/display/JIRA/Supported+Platforms) for further information.

### Configuration

We don't provide any dynamic configuration by using environment variable; by the way, since this Docker container is created by using Ansible Container with [Ansible Role for JIRA](https://github.com/alvistack/ansible-role-jira), you could create a playbook for your customization, retouch the running Docker instance, then restart it:

    ansible-playbook \
        -i jira,
        -c docker
        /path/to/playbook.yml
    docker restart jira

Upgrade
-------

To upgrade to a more recent version of JIRA Server you can simply stop the `jira` container and start a new one based on a more recent image:

    docker stop jira
    docker rm jira
    docker pull alvistack/ansible-container-jira
    docker run ... (See above)

As your data is stored in the data volume directory on the host it will still be available after the upgrade.

*Note: Please make sure that you **don't** accidentally remove the `jira` container and its volumes using the `-v` option.*

Backup
------

For evaluations you can use the built-in database that will store its files in the JIRA Server home directory. In that case it is sufficient to create a backup archive of the directory on the host that is used as a volume (`/var/atlassian/application-data/jira` in the example above).

Versioning
----------

The `latest` tag matches the most recent version of this repository. Thus using `alvistack/ansible-container-jira:latest` or `alvistack/ansible-container-jira` will ensure you are running the most up to date version of this image.

Dependencies
------------

[requirements.yml](requirements.yml)

License
-------

-   Code released under [Apache License 2.0](LICENSE)
-   Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

Author Information
------------------

-   Wong Hoi Sing Edison
    -   <https://twitter.com/hswong3i>
    -   <https://github.com/hswong3i>


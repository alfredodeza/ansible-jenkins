ansible-jenkins
===============
An ansible module to control a Jenkins server. Currently supports:

* node management (via `jenkins-node` module)

This module requires the `python-jenkins` package, available from PyPI.

`jenkins-node`
==============
This module provides some management features to control Jenkins
nodes.

options
-------

*  uri:
    - description:  Base URI for the Jenkins instance
    - required: true

*  username:
    - description:  The username to log-in with.
    - required: true

*  password:
    - description:  The password to log-in with.
    - required: true

*  operation:
    - description:  Operation to perform
    - required: false
    - default: 'create'
    - choices: [ create, delete, enable, disable ]

*  name:
    - description: Node name
    - required: true

*  executors:
    - description:  Number of executors in node
    - required: false
    - default: 2

*  description:
    - description:  Description of the node
    - required: false
    - default: null

*  labels:
    - description:  Labels to associate with a node, like "amd64" or "python"
    - required: false
    - default: null

*  exclusive:
    - description:  Mark this node for tied jobs only
    - required: false
    - default: 'no'
    - choices: ['no', 'yes']


Launcher and Launcher Parameters
--------------------------------

*  launcher:
    - description: Launcher method for a remote node (only needed for 'create' operations)
    - required: false
    - default: 'hudson.plugins.sshslaves.SSHLauncher'

*  remoteFS:
    - description: Path to the directory used for builds
    - required: false

*  credentialsId:
    - description: the ID of the user needed for authentication. Usually found in
        credentials.xml or via the url {host}/credential-store/domain/_/credential/{id}

*  host:
    - description: hostname or IP for the host to connect to the slave

* port:
    - description:  The TCP port on which the slave's SSH daemon is listening, usually 22.
    - default: 22

* maxNumRetries:
    - description: Set the number of times the SSH connection will be retried if
          the initial connection results in an error. If empty, retrying will be
          disabled.
    - default: 0

* retryWaitTime:
    - description: Set the number of seconds to wait between retry attempts of
          the initial SSH connection. Only used if ``maxNumRetries`` is
          enabled.
    - default: 0


examples
--------
Create new node::

    - name: Create new node
      jenkins-node: uri={{ jenkins_uri }} username={{ user }} password={{ password }}
               name={{ node_name }} operation=create

Delete an existing node::

    - name: Delete a node
      jenkins-node: uri={{ jenkins_uri }} username={{ user }} password={{ password }}
               name={{ node_name }} operation=delete

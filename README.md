# Ansible Role `locust_slave`

Manages locust.io slaves.

## Requirements

Locust.io requires ZeroMQ. This role will therefor install
zeromq-devel and gcc system-wide to compile the necessary python
pips for Locust.io. The upstream ZeroMQ yum repository will be
registered and enabled to do this.

All python related software requirements will be auto-installed
inside a virtualenv.

## Role Variables

| Variable        | Default   | Comments (type)                              |
| :---            | :---      | :---                                         |
| `instance_name` | `slave`   | Name to distiguish between instances.        |
| `instance_data` |           | Path to data to be copied into instance dir  |
| `master_host`   |           | IP, hostname or FQDN of the Locust.io master |
| `master_port`   | 5557      | TCP portnumber of the Locust.io master       |
| `locustfile`    |           | The Locust.io scenario file to play          |
| `state`         | `started` | State of Locust.io on the host.              |
| `csv`           |           | Base name of CVS report files                |
| `logfile`       |           | Filename of the Locust.io logfile            |
| `loglevel`      |           | Locust.io log level                          |

The `state` parameter can be one of:

* `present` - Locust.io should be installed in it's own virtualenv
* `started` - Locust.io should be up and running
* `restarted` - Locust.io should be freshly restarted
* `stopped` - Locust.io should be stopped
* `absent` - Locust.io should not be installed

A directory named `/opt/locust.io` will be created. Inside of it, a
subdirectory per instance will be created. If `state` is set to `absent`,
this directory will be removed.

The `instance_data` parameter can point to a file or directory to
be copied into the instance subdirectory. For example, `instance_data: data/`
would copy the `data/` directory inside your playbook's `files/` directory
to the instance subfolder.

You can specify the `locustfile` parameter as a path relative to the
`instance_data` content root. (see example below)

## Operating Systems

This role was developed and tested for CentOS 7.4.

## Dependencies

None

## Example Playbook

To have a running Locust.io slave you could do this:

    - hosts: locust_slaves
      tasks:
      - include_role:
           name: tinx.locust_slave
        vars:
           master_host: 'locust_master.example.com'
           instance_data: data/
           locustfile: 'stress-test-prod.py'

## Testing

Molecule tests are provided. Naturally, they require additional dependencies.

## License

BSD

## Author Information

 - [Andreas Jaekel](https://github.com/tinx/)

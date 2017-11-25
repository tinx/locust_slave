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

| Variable                             | Default  | Comments (type)                                   |
| :---           | :---             | :---                                              |
| `install_path` | `/opt`    | Where the Locust.io files should exist.      |
| `master_host`  |           | IP, hostname or FQDN of the Locust.io master |
| `master_port`  | 5557      | TCP portnumber of the Locust.io master       |
| `locustfile`   |           | The Locust.io scenario file to play          |
| `state`        | `started` | State of Locust.io on the host.              |

The `state` parameter can be one of:

* `present` - Locust.io should be installed in it's own virtualenv
* `started` - Locust.io should be up and running
* `restarted` - Locust.io should be freshly restarted
* `stopped` - Locust.io should be stopped
* `absent` - Locust.io should not be installed

A directory named `locust.io` will be created at the `install_path`. If
`state` is set to `absent`, this directory will be removed from the
`install_path`.

## Dependencies

None

## Example Playbook

To have a running Locust.io slave, installed in it's own VirtualEnv
in `/usr/local/locust.io`, you could do this:

    - hosts: locust_slaves
      tasks:
      - include_role:
           name: tinx.locust_slave
        vars:
           install_path: '/usr/local'
           master_host: 'locust_master.example.com'
           locustfile: '/home/locust/stress-test-prod.py'

## Testing

Molecule tests are provided. Naturally, they require additional dependencies.

## License

BSD

## Author Information

 - [Andreas Jaekel](https://github.com/tinx/)

# Ansible Role `locust_slave`

Manages locust.io slaves.

## Requirements

none

## Role Variables

| Variable                             | Default  | Comments (type)                                   |
| :---           | :---             | :---                                              |
| `install_path` | `/opt/locust.io` | Where the Locust.io files should exist.   |
| `master_host`  |                  | IP, hostname or FQDN of the Locust.io master     |
| `master_port`  | 5557             | TCP portnumber of the Locust.io master           |
| `locustfile`   |                  | The Locust.io scenario file to play              |
| `state`        | `started`        | State of Locust.io on the host.                  |

The `state` parameter can be one of:

* `present` - Locust.io should be installed in it's own virtualenv
* `started` - Locust.io should be up and running
* `restarted` - Locust.io should be freshly restarted
* `stopped` - Locust.io should be stopped
* `absent` - Locust.io should not be installed

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
           install_path: '/usr/local/locust.io'
           master_host: 'locust_master.example.com'
           locustfile: '/home/locust/stress-test-prod.py'

## Testing

Molecule tests are provided. Naturally, they require additional dependencies.

## License

BSD

## Author Information

 - [Andreas Jaekel](https://github.com/tinx/)

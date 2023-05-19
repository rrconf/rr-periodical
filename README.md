# periodical

This module manages `systemd` timers for modules providing the `systemd.timer` file in the root of their repository. Optionally a `systemd.service` file in module's root directory can be used. Please see the [systemd.timer(5)](https://manpages.debian.org/systemd.timer.5.html) and [systemd.service(5)](https://manpages.debian.org/systemd.service.5.html) documentation for more information.

## Invocation

    require periodical [enable/disable] rrconf_module_name

The `periodical` module first fetches the named module and checks if it contains the `systemd.timer` file. If there is no timer file present, it will not touch the systemd configuration at all. The following arguments can be used:

### enable

The `enable` argument installs the `systemd.timer` file in `/etc/systemd/system/` and renames it to `{rrconf_module_name}.timer`. If the `systemd.service` file is present, it will be copied to `/etc/systemd/system/` and renamed to `{rrconf_module_name}.service`. If there is no service file, a stock service file will be generated instead. Finally, the timer will be enabled and started.

### disable

The `disable` argument disables and removes the timer and service files, and reloads the systemd daemon.

### TODO

Currently, there is no way to specify the `OnCalendar=` value on the executing host, so the defaults in the repository of the executed module are used. If you would like to add this functionality, please submit a patch.

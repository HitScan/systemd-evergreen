# systemd-evergreen
Sample Evergreen startup scripts for use on systemd based distributions

Included are systemd service units for opensrf/evergreen, clark-kent, oils-sip, oils-z3950, and websocketd. As defined all included services require opensrf, and will restart if it restarts. To loosen this restriction edit the [Install] sections of the appropriate units.

# Installation
Copy all .service files to /etc/systemd/system/ and then run systemctl daemon-reload as root. To enable services to run at startup, run systemctl enable <service list> for the desired services. To flexibly support multiple types of installations the only service required is opensrf.

# Customization
Several things that can be specified on the command line are now changed via drop-in files. For example, to change the lockfile used by clark-kent.service, create the directory /etc/systemd/system/clark-kent.service.d/ and put an override.conf file in it with the value Environment=LOCKFILE=/some/other/value. See the Environment entries in each service file to see what can be customized.

# Changes From Stock Install
When using oils_ctl.sh to start the SIP or Z39.50 servers you can specify a pid file location. Because this is primarily only used by oils_ctl.sh to (inaccurately, in the case of a crash) determine if a service is running, these pid files aren't used with systemd.
Also, the SIP and Z39.50 servers now log all output to the journal/syslog. Because of the number of separate opensrf services started by osrf_control those stdout log files are still used.

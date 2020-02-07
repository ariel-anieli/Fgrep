# Fgrep

Greps through FortiManager or FortiGate configurations, and prints matching extracts.

## Examples
If _config_ contains the match.
```
# ssh ${USER}@${HOST} "show" | Fgrep -v key="interface"
config system interface
    edit "port1"
        set ip 10.70.11.218 255.255.240.0
        set allowaccess ping https ssh telnet http
    next
    edit "port2"
    next
    edit "port3"
    next
    edit "port4"
        set ip 10.0.0.1 255.255.255.0
        set allowaccess ping https ssh telnet http
    next
end
```

If it is _edit,_
```
# ssh ${USER}@${HOST} "show" | Fgrep -v key="port4"
config system interface
    edit "port4"
        set ip 10.0.0.1 255.255.255.0
        set allowaccess ping https ssh telnet http
    next
end
```

Or _set_,
```
# ssh ${USER}@${HOST} "show" | Fgrep -v key="10.0.0.1"
config system interface
    edit "port4"
        set ip 10.0.0.1 255.255.255.0
    next
end
```

Or even, when many items match the search, Fgrep gives path to each location:
```
# ssh ${USER}@${HOST} "show" | Fgrep -v key="ip "
config system interface
    edit "port1"
        set ip 10.70.11.218 255.255.240.0
    next
    edit "port4"
        set ip 10.0.0.1 255.255.255.0
    next
end
config system syslog
    edit "Myself"
        set ip "10.70.0.1"
    next
end
```

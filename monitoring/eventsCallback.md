# EventsCallback

The health framework now support callout scripts for events. Simply install 
the /var/mmfs/etc/eventsCallback script and make it executable. Then it will
be called with the following arguments whenever an event is raised:

* version -- integer
* date -- yyyy-mm-dd
* time -- hh:MM:ss.mmm
* timezone -- GMT, CET, CEST, ...
* event -- event name from /usr/lpp/mmfs/lib/mmsysmon/*.json
* component -- GPFS, FILESYSTEM, NODE, custom, ...
* identifier -- fs1, gpfs0, ...
* severity -- TIP, INFO, WARNING, ERROR
* state -- *H*ealthy, *T*ips, *D*egraded, *E*rror or *X*
* message -- 'Single quoted message'
* event_arguments -- Comma separated list of %-encoded, single quoted arguments

Example:

```
# cat > /var/mmfs/etc/eventsCallback << 'EOF'
#! /bin/sh -
cat <<'EOF' 
echo $* > /tmp/eventsCallback.log

EOF

# chmod +x /var/mmfs/etc/eventsCallback
# mmsysmonc event custom event_1 a,b
# cat /tmp/eventsCallback.log

```


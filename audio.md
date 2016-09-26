## Set default sink
http://askubuntu.com/a/72076
```
# 
pacmd list-sinks
# Set sink to sink index 1
# Can use `name:` field returned by `pacmd list-sinks`
pacmd set-default-sink 1

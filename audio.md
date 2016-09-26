## Set default sink
http://askubuntu.com/a/72076
```
# 
pacmd list-sinks
 index: 1
	name: <alsa_output.pci-0000_00_1b.0.analog-stereo>

# Set sink to sink index 1
# Can use index or name: field value shown by `pacmd list-sinks`
pacmd set-default-sink "<alsa_output.pci-0000_00_1b.0.analog-stereo>"

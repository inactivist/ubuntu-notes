# ubuntu-notes
## Troubleshooting
### Audio
#### No audio devices showing in audio control panel?  
``` 
pulsaudio -vvv
...
E: [pulseaudio] module-ladspa-sink.c: Master sink not found
E: [pulseaudio] module.c: Failed to load module "module-ladspa-sink" (argument: "sink_name=ladspa_output.mbeq_1197.mbeq master=bluez_sink.B8_69_C2_30_E6_54 plugin=mbeq_1197 label=mbeq control=7.0,7.0,7.0,3.5,3.0,3.0,3.0,1.5,0.0,-2.0,-3.5,-6.0,-9.0,-1.0,0.0"): initialization failed.
E: [pulseaudio] main.c: Module load failed.
E: [pulseaudio] main.c: Failed to initialize daemon.
```
This answer on SO seems to do the trick.  [Delete ~/.config/pulse and restart pulseaudio.](http://askubuntu.com/a/549228/116968)

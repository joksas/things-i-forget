# Things I Forget

## Setting Up Sound Devices

Setting up sound devices is incredibly frustrating in Linux. On rare occasions when one manages to configure ALSA, some programs still won't work because they require PulseAudio. Some programs won't even tell you that they want PulseAudio and just break without explanation (I'm looking at you MS Teams). But PulseAudio may sometimes ignore ALSA configs and/or introduce a hundred new sinks/sources (no, I don't want to use my mic as a speaker).

I found that [pavucontrol](https://archlinux.org/packages/extra/x86_64/pavucontrol/) is the most straightforward way to set up audio devices. Just open it, go to "Configuration" tab and

* set the devices that you won't be using as "Off"
* set mics as inputs, e.g. "Analog Stereo Input"
* set headphones/speakers as outputs, e.g. "Analog Stereo Output"

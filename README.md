# Things I Forget

## Setting Up Sound Devices

Setting up sound devices is incredibly frustrating in Linux. On rare occasions when one manages to configure ALSA, some programs still won't work because they require PulseAudio. Some programs won't even tell you that they want PulseAudio and just break without explanation (I'm looking at you MS Teams). But PulseAudio may sometimes ignore ALSA configs and/or introduce a hundred new sinks/sources (no, I don't want to use my mic as a speaker).

I found that [pavucontrol](https://archlinux.org/packages/extra/x86_64/pavucontrol/) is the most straightforward way to set up audio devices. Just open it, go to "Configuration" tab and

* set the devices that you won't be using as "Off"
* set mics as inputs, e.g. "Analog Stereo Input"
* set headphones/speakers as outputs, e.g. "Analog Stereo Output"

## USB Sticks

[udiskie](https://archlinux.org/packages/community/any/udiskie/) makes it very easy to mount and unmount USB devices. I like it because I don't need to specify device names or mount points. However, if you are handling more than one device at a time, you might need to specify its name when unmounting (unless you are fine with unmounting all of them at once).

To mount all handleable devices
```console
$ udiskie-mount -a
```

To unmount all handleable devices
```console
$ udiskie-umount -a
```

## Updating Large Directories

When I have to update large (often remote) directories where only a few files have changed, `cp` isn't the best solution. I prefer [rsync](https://archlinux.org/packages/extra/x86_64/rsync/):
```console
$ rsync -ru --delete source/ destination
```

## Updating LaTeX packages

Distributions like TeX Live are useful, but sometimes one may want to use the newest version of a particular LaTeX package. For that, you can use `tllocalmgr` or `tlmgr` -- see [this](https://wiki.archlinux.org/title/TeX_Live#tllocalmgr) for more info. For example, to update [siunitx](https://ctan.org/pkg/siunitx), one would do
```console
$ tllocalmgr update siunitx
```

## Searching Inside Files

To recursively search for a `pattern` inside files of a directory identified by a `path`, do
```console
$ grep -rn 'path' -e 'pattern'
```

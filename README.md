# Things I Forget

## Setting Up Sound Devices

Setting up sound devices is incredibly frustrating in Linux. On rare occasions when one manages to configure ALSA, some programs still won't work because they require PulseAudio. Some programs won't even tell you that they want PulseAudio and just break without explanation (I'm looking at you MS Teams). But PulseAudio may sometimes ignore ALSA configs and/or introduce a hundred new sinks/sources (no, I don't want to use my mic as a speaker).

I found that [pavucontrol](https://archlinux.org/packages/extra/x86_64/pavucontrol/) is the most straightforward way to set up audio devices. Just open it, go to "Configuration" tab and

* set the devices that you won't be using as "Off"
* set mics as inputs, e.g. "Analog Stereo Input"
* set headphones/speakers as outputs, e.g. "Analog Stereo Output"

## USB Sticks

### Simple mounting

[udiskie](https://archlinux.org/packages/community/any/udiskie/) makes it very easy to mount and unmount USB devices. I like it because I don't need to specify device names or mount points. However, if you are handling more than one device at a time, you might need to specify its name when unmounting (unless you are fine with unmounting all of them at once).

To mount all handleable devices
```console
$ udiskie-mount -a
```

To unmount all handleable devices
```console
$ udiskie-umount -a
```

### Mounting with NTFS target filesystem

```console
$ mount -t ntfs /path/to/device /path/to/mount/point
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

## Okular Movements

After clicking on an internal hyperlink, you are redirected to a different page. To move back, use <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>Left</kbd>. To move forward, use <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>Right</kbd>.

## Making PDFs Searchable

If a PDF contains scanned documents, one can OCR it using [ocrmypdf](https://pypi.org/project/ocrmypdf/). On Arch, do
```console
$ pacman -S tesseract tesseract-data-eng
$ pip install ocrmypdf
$ ocrmypdf input.pdf output.pdf
```

## TensorFlow GpuSolver Error

If you get something like
```text
Creating GpuSolver handles for stream 0x4dd54270
Check failed: cusolverDnCreate(&cusolver_dn_handle) == CUSOLVER_STATUS_SUCCESS Failed to create cuSolverDN instance.
Abort (core dumped)
```
then do
```python
devices = tf.config.experimental.list_physical_devices("GPU")
for device in devices:
    tf.config.experimental.set_memory_growth(device, True)
```

## Delete Folder from S3

To recursively delete files in a "folder" on S3 storage, do
```console
$ s3cmd rm --recursive --force s3://bucket/folder
```

## Convert LaTeX to W*rd

You can use [pandoc](https://pandoc.org):
```console
$ pandoc -F pandoc-crossref -M autoEqnLabels --citeproc --bibliography=bibliography.bib -s main.tex -o main.docx
```

Can even provide [citation style](https://github.com/citation-style-language/styles):
```console
$ pandoc -F pandoc-crossref -M autoEqnLabels --citeproc --bibliography=bibliography.bib --csl=nature.csl -s main.tex -o main.docx
```

## Make space for Arch packages

I didn't make a large enough partition for my Arch packages (sad!). To clean up cache, do
```console
$ yay -Scc
```

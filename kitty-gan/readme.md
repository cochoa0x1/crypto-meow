# Generate new cat images!

1. Naive approach: svg-> numpy array, generate new numpy array, i.e., don't bother using any of the detailed svg info.

The first issue: working with the svg files, as these are just text we need to convert them to images. I tried to use cairo but was experiencing some parsing errors so I ended up using [Wand](http://docs.wand-py.org/en/0.4.4/) a wrapper for imagemagick.

```bash
$ apt-get install libmagickwand-dev
$ pip install Wand
```

to convert the frames to video:

```bash
ffmpeg -i cats/%4d.png output.mp4
```

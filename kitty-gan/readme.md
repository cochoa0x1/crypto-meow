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

#### model is live here!
https://cochoa0x1.github.io/crypto-meow/kitty-gan/


#### here is a video of the training process!

[![](https://img.youtube.com/vi/bsDgN9w8P20/0.jpg)](https://www.youtube.com/watch?v=bsDgN9w8P20)


## Problems and FAQ

###Message “mogrify: delegate library support not built-in”

`mogrify: delegate library support not built-in './foobar.tiff' (LCMS) @ warning/profile.c/ProfileImage/837.`

*mogrify* is part of ImageMagick, an the *delegate library* is part of [LitteCMS](http://www.littlecms.com/). Your local ImageMgaick must be compiled with litte-cms2 support. Reinstall imagemagick according to this [solution](https://github.com/Homebrew/legacy-homebrew/issues/16619):

```bash
$ brew remove imagemagick
$ brew install little-cms2 imagemagick --with-little-cms2
```


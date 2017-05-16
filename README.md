# negatives/linear-tiff

**Converts RAW/NEF/CR2 files into linear TIFF files. Features:**

- **Mirroring:** Useful for negatives digitalized on their emulsion side. 
- **Resizing:** When megapixel power is not needed
- **Grayscaling:** B/W lovers save up to 60% disk space. 
- **ICC profiles:** Output images get a linear gamma profile. No ‘custom gamma’ needed in Photoshop!

These utilities are used:

- [dcraw:](cybercom.net/~dcoffin/dcraw/dcraw.1.html) Raw to linear TIFF conversion
- [GNU Parallel:](https://www.gnu.org/software/parallel/) Use all CPU cores for maximum speed
- [ImageMagick:](https://www.imagemagick.org/script/index.php)  B/W grayscaling, TIFF resizing, ZIP compression

Requirements:

- [Homebrew](https://brew.sh/) Package manager for OS X
- [tomkyle/homebrew-negatives](https://github.com/tomkyle/homebrew-negatives) Homebrew tap for negatives-related scripts.

## Homebrew Installation (OS X)


The *linear-tiff* bash script can be installed by a Homebrew formula, which itself is part of the [tomkyle/homebrew-negatives](https://github.com/tomkyle/homebrew-negatives) tap. 

```bash
# Install tap, optionally
$ brew tap tomkyle/negatives

# Install formula
$ brew install linear-tiff
```

As “tapping” first is not neccessarily needed, you can install the formula directly:

```bash
$ brew install tomkyle/negatives/linear-tiff
```

# Usage

Run *linear-tiff* without parameters to get a short help text:

```bash
$ linear-tiff [options] [-a | file(s)]
```

## Options

Option | Value | Description
:------|:------|:------------
-a     |       | All images — process any RAW/NEF/CR2 file in working directory, using GNU Parallel.
-d     |       | Desaturate colors — recommended for B/W negatives. dcraw's TIFF output is converted to 16-bit grayscale, with a linear gamma 1.0 ICC profile applied (Gray-elle-V4-g10.icc). Grayscaling saves up to 60% in file size. 
-f     | value | Mirror the image vertically and/or horizontally. Possible values are `flop`, `flip` or even `flipflop`. Example: `-f flop`
-o     | path  | Output directory — default is current working directory. Example: `-o results`
-r     | pixel | Resize  image — pixel width for larger side, preserving aspect ratio. Example: `-r 3000`
-v     |       | Verbous mode — show some more information under way.




## Upcoming Features

These features go into the current major version 1:

-  **Long option names:** Those preferring speaking option names like `--resize` or `--all` will enjoy the long option names I currently am working on. 

- **Filter by star rating:** Many photo managers like Lightroom or Bridge let their users rate images with ‘stars’ or reject them. *linear-tiff* will get a new CLI option flag to set a minimum rating level. 

- **Custom configuration files:** What if users could store their favourite options in a configuration file? `~/.negativesrc` or ` ~/linear-tiff.conf` or even an *INI, YAML* or *JSON?*



## Roadmap to Version 2


- **The *-r* option will be renamed to *-w*,** as *-r* is more natural for the upcoming *Rating filter*, and so is *-w* for *width*.
- **The *-f* option will be renamed to *-m*,** as the image action actually performed is *mirroring horizontally or vertically*. The option values *flip* and *flop* will then become something like *V*, *H* or *VH*.



                              
## Problems and FAQ

### linear-tiff does not find my Raw photos in batch mode.

Not neccessarily your fault. While *dcraw* itself can defacto handle every existing RAW photo file extensions, *linear-tiff* uses the *find* command with a regex to get a list of files to work on. So we have a question of “how long is the regex”. — For now, these most-occuring file extensions are implemented in *linear-tiff:*

- NEF (Nikon)
- CR2 (Canon)
- RAW (Contax, Kodak, Leica, Panasonic)

[Drop me a line](https://github.com/tomkyle/negatives-linear-tiff/issues) to “order” your favourite file extension. I'll happily lengthen the regex to your needs :smiley:



### Message “mogrify: delegate library support not built-in”

`mogrify: delegate library support not built-in './foobar.tiff' (LCMS) @ warning/profile.c/ProfileImage/837.`

*mogrify* is part of ImageMagick, an the *delegate library* is part of [LitteCMS](http://www.littlecms.com/). Your local ImageMgaick must be compiled with litte-cms2 support. Reinstall imagemagick according to this [solution](https://github.com/Homebrew/legacy-homebrew/issues/16619):

```bash
$ brew remove imagemagick
$ brew install little-cms2 imagemagick --with-little-cms2
```

# Alephbeis Sans Build Process

To create autohinted TrueType font files in the command line, install the following tools:

- [fontmake](https://github.com/googlefonts/fontmake)
- [gftools](https://github.com/googlefonts/gftools)

Use `fontmake` to generate the TrueType files from the Glyphs source:

```bash
fontmake -g AlephbeisSans.glyphs -i -a -o ttf --output-dir ttf
```

Change to ttf directory:

```bash
cd ttf
```

Run `gftools` to add DSIG:

```bash
gftools fix-dsig --autofix *.ttf
```

Run `gftools` to fix hinting issue:

```bash
for f in *.ttf; do gftools fix-hinting "$f"; done
rm *.ttf
for f in *.fix; do mv "$f" "${f/.ttf.fix/.ttf}"; done
```

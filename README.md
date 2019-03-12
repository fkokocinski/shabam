# shabam
A python tool to plot BAM or CRAM sequence reads.

## Installation
install [cairo](https://www.cairographics.org/download/) if not already
installed:
```sh
# macOS via conda, or via homebrew (choose one, then set the library path)
conda install cairo; CAIRO=`conda info --root`/pkgs/cairo-1.14.8-0/lib
brew install cairo; CAIRO=`brew --prefix cairo`
export DYLD_LIBRARY_PATH=${CAIRO}
```

Install this version of shabam:
```sh
pip install git+git://github.com/fkokocinski/shabam.git --user
```

## The orginal version
```py
from shabam import seqplot
seqplot('example.bam', chrom='1', start=30243, end=30321,
    fastafile='reference.fasta', out='plot.svg')
```

![Reality](/tests/data/reality.svg)

### Plotting options
- shade reads by strand with `by_strand=True`
- plot multiple sequence files together with a list of paths e.g.
  `['child.bam', 'mom.bam', 'dad.bam']`
- export PDF, PNG, SVG or PS formatted plots with matching filename extensions
- seqplot returns PNG data if you don't include an output filename

### Command line version
```sh
./bin/shabam.py \
  --seqfiles example.bam \
  --chrom 2 \
  --start 30243 \
  --end 30321 \
  --fastafile reference.fasta \
  --out plot.svg
```

## Modification in this fork
- [ ] Write the base identity of the reference sequence into the plot
- [ ] Write the base identity of the reads into the plot where there are changes to the reference. Write '.' for matching bases.
- [ ] Use 1-based system to label the referce.
- [ ] Option to write the name of the reference sequence and of each read next to the sequences. The width of the image is slightly increased for this. If multiple reads are plotted in a line, only the first name is used.
- [ ] For insertions only write out the extra bases, not additionally the next reference base.

Example call:
```
seqplot('example.bam', chrom='1', start=30243, end=30321,
    fastafile='reference.fasta', out='plot.svg', add_names=True)
```
Example output:
![Reality](/tests/data/reality2.png)


## Credit
Further info at the source repo of [Daniel Rice](https://github.com/dlrice/shabam)

Initial cigar parsing code lifted with permission from
[pybamview](https://github.com/mgymrek/pybamview).

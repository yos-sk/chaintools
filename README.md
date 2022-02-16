# chaintools: utilities for the genomic chain format

This toolkit provides utilities to process whole-genome maps in the ([chain format](https://genome.ucsc.edu/goldenPath/help/chain.html)).

## Install

```
git clone git@github.com:milkschen/chaintools.git
```

### Dependencies:
* [intervaltree](https://github.com/chaimleib/intervaltree)
```
# conda
conda install -c conda-forge intervaltree
# pip
pip install intervaltree
```
* [pandas](https://pandas.pydata.org)
```
# conda
conda install -c anaconda pandas
# pip
pip install pandas
```


## Usage

### Annotate
Annotate a chain file:
* Specify the contig and start/end positions of each segment
* Calculate the identity of each segment (optional)
* Write liftable regions to a pair of BED files (one for source and one for target) (optional)

```
# Annotate contig and positions
python src/annotate.py -c <in.chain> -o <out.chain>
# Add identity
python src/annotate.py -c <in.chain> -o <out.chain> -fs <source.fasta> -ft <target.fasta>
# Also write liftable regions to BED files
python src/annotate.py -c <in.chain> -o <out.chain> -fs <source.fasta> -ft <target.fasta> -b <bed_prefix>
```


### Invert
Invert a chain file by switching the source and dest references

```
python src/invert.py -c <in.chain> -o <out.paf>
```


### Convert to PAF
Convert a chain file to the ([PAF format](https://github.com/lh3/miniasm/blob/master/PAF.md)). 

The source chain is converted as the query sequence and the target chain is converted as the target sequence.

```
python src/to_paf.py -c <in.chain> -o <out.paf>
```


### Convert to VCF
Convert to chain file to the VCF format

```
python src/to_vcf.py -c <in.chain> -s <source.fa> -t <target.fa> -o <out.vcf>
```


### Convert to SAM
Convert a chain file to the SAM format

```
python src/to_sam.py -c <in.chain> -s <source.fa> -t <target.fa> -o <out.sam> 
```


### Filter
Filter a chain file by critera including chain sizes and overlap status. 
The size of a chain is the sum of all its segments, including matches and mismatches. The overlap filter makes sure no chains overlap wrt either source or target references. If two chains overlap, the smaller one is removed.

```
# Filter by chain size
python src/filter.py -c <in.chain> -o <out.filtered.chain> -s <size>
# Filter by both chain size and overlap status
python src/filter.py -c <in.chain> -o <out.filtered.chain> -u -oc <out.overlapped.chain> -s <size>
```

### Stats
Calculate summary statistics of a chain file

```
python src/stats.py -c <in.chain> -o <stats.tsv>
```

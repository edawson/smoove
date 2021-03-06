v0.2.1
======
+ fix bug in smoove duphold for samples > threads that resulted in stalling
+ smoove is now more discerning about reads that are soft-clipped on both ends as
  these could be due to inversions. if a read is not flipped relative to its mate
  and it is soft-clipped on both ends, it is still removed.
+ in some cases reads with a large NM (mismatches) were not filtered because they
  had an unexpected type (uint8). `smoove` now checks more types and for some bams
  will remove more records which improves specificity.
+ smoove will now be more conservative with `NM` counting. an insertion of 7 bases
  is counted as an NM of 7. smoove will now correct this to an NM of 1 so it counts
  the number of events rather than the number of bases of each event.
+ simplify rules for filtering and make them less strict.

v0.2.0
======
+ **add [duphold](https://github.com/brentp/duphold)** annotations. (requires duphold v0.0.4)

v0.1.11
=======
+ flip start and end for small percent of cases where that's a problem
+ expose min sample weight to allow adjusting required support for each variant

v0.1.10
======= 
+ fix type in annotate (s/Number/Integer/)

v0.1.9
======
+ better error message in merge.
+ use set -e in process calls so we don't exit with 0 even on failure

v0.1.8
======
+ don't use --sum in merge step. this reduces the size of CI when using `smoove merge`

v0.1.7
======
+ add a `SHQ`: `smoove het-quality` score to the FORMAT field and a `MSHQ`:`mean smoove het-quality` score
  to the INFO. Variants with a het-quality of 4 are quite good.

v0.1.6
======
+ sensitivity improvement by dropping reads with > 5 mismatches.

v0.1.5
======
+ sensitivity increases for variants without split reads.
+ use a fixed length of 4 in merge (gives much better merging)
+ add new annotate command which takes a gff and annotates with gene names
+ increase max_reads argument to svtyper to reduce false negatives
+ remove QCFail and duplicate reads from split and disc.bams. This is now
  part of `smoove` but also fixed in `lumpy_filter` upstream.

v0.1.4
======
+ fix bug when using `-x/--removepr` with `--genotype` (thanks @brad for test-case)

v0.1.3
======
+ update command to match latest mosdepth

v0.1.2
======
+ bcftools and gsort are now required.
+ output never goes to STDOUT
+ output contigs to header
+ add svtools to docker
+ add option to remove PRPOS and PREND

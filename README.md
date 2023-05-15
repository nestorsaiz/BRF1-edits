## hg38 reference genome modification

We wanted to edit the reference genome hg38 to collapse the repeat found in the intron of the gene *BRF1* (found at position chr14:105,229,547-105,240,946). The presence of a ~100-mer repeat in this region makes mapping to it difficult. 

After looking at the locus, we determined that the repeat, whose units are not entirely identical, has 5 units that are repeated 49x, 33x, 12x, 6x and 5x, respectively, as well as 6 unique units. The differences between these are most typically 1-2bp, with some having 3-4bp mutated. The units present more than once are 1-2bp apart each, and together comprise 95% of the locus. The 6 unique units are 3bp apart. The most divergent unit is that located adjacent to the preceding 5' exon, which has at least 20bp of difference (referred to as Flank 1 below). The 3' end of the repeat (referred to as Flank 2) is one of the 49x units.

Given the above, we decided to create a v1 edited reference comprising the following, after the 5' exon:
- Flank 1 (5' unit,  most divergent repeat unit)
- 49x unit (which includes the target of the TLP1c probe, CGCCCAGCTGGGGGCGGGGGA)
- Flank 2 (3'49x unit, also includes the target of TLP1c)

With the following linear arrangement:
...5' exon][Flank 1][49x unit][Flank 2 (49x unit)][3'exon...

This design ensures that, when mapping reads to this reference, all the following boundaries are present: 
- 5' exon-Flank 1 boundary
- Flank 1-49x repeat boundary
- 49x-49x repeat boundary
- Flank 2-3' exon boundary

The edit was made using the [reform tool](https://gencore.bio.nyu.edu/reform/) built by the Genomics Core at NYU CGSB 

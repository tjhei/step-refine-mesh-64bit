# step-refine-mesh-64bit

A small deal.II example program to test adaptive mesh refinement with a large number of cells (>4^32) to test correct treatment of large problems.

Refinement is done based on a fake estimator using ``cell->center()*sqrt(cell->diameter)``.

Results from running on Frontera, nodes=40, cores=2240, RAM=192GB/node

refine_and_coarsen_fixed_number:

| n_global_active_cells | increase | n_global_levels | ghost_owners.size | level_ghost_owners.size | workload_imbalance | Memory tria/mb | Refine time/s |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 419,430,400           |          |              12 |                 2 |                      10 |            1.00003 |             47 |          1.05 |
| 671,088,568           |  1.60000 |              13 |                 2 |                       9 |            1.75003 |             71 |          4.88 |
| 1,073,743,099         |  1.60000 |              14 |                 2 |                       8 |            2.50002 |            118 |          8.32 |
| 1,717,989,982         |  1.60000 |              14 |                 2 |                       7 |            2.50000 |            197 |          14.5 |
| 2,748,782,788         |  1.60000 |              15 |                 2 |                       6 |            3.25000 |            282 |          23.5 |
| 4,398,050,704         |  1.60000 |              15 |                 2 |                       5 |            3.25000 |            473 |          46.3 |
| 7,036,878,589         |  1.60000 |              15 |                 2 |                       4 |            3.25000 |            791 |          81.1 |
| 11,259,001,246        |  1.60000 |              16 |                 2 |                       4 |            4.00000 |           1241 |           103 |
| OOM                   |          |                 |                   |                         |                    |                |               |


refine_and_coarsen_fixed_fraction:

| n_global_active_cells | increase | n_global_levels | ghost_owners.size | level_ghost_owners.size | workload_imbalance | Memory tria/mb | Refine time/s |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 419,430,400           |          |              12 |                 2 |                      10 |               1.00 |             47 |          1.05 |
| 496,213,144           |  1.18306 |              13 |                 2 |                       9 |               1.75 |             56 |          3.97 |
| 598,332,343           |  1.20580 |              13 |                 2 |                       9 |               1.75 |             65 |          4.24 |
| 730,754,998           |  1.22132 |              14 |                 2 |                       9 |               2.50 |             76 |          6.18 |
| 898,515,409           |  1.22957 |              14 |                 2 |                       8 |               2.50 |            104 |          8.63 |
| 1,109,076,427         |  1.23434 |              14 |                 2 |                       8 |               2.50 |            121 |          9.42 |
| 1,373,343,307         |  1.23828 |              14 |                 2 |                       7 |               2.50 |            143 |         12.20 |
| 1,705,889,674         |  1.24214 |              14 |                 2 |                       7 |               2.50 |            197 |         15.60 |
| 2,125,659,025         |  1.24607 |              14 |                 2 |                       6 |               2.50 |            232 |         18.20 |
| 2,653,984,501         |  1.24855 |              15 |                 2 |                       6 |               3.25 |            277 |         26.30 |
| 3,312,956,263         |  1.24830 |              15 |                 2 |                       6 |               3.25 |            386 |         31.40 |
| 4,134,164,215         |  1.24788 |              15 |                 2 |                       5 |               3.25 |            454 |         40.00 |
| 5,159,707,060         |  1.24807 |              15 |                 2 |                       5 |               3.25 |            540 |         50.70 |
| 6,445,150,246         |  1.24913 |              15 |                 2 |                       4 |               3.25 |            751 |         62.50 |
| 8,062,657,429         |  1.25097 |              15 |                 2 |                       3 |               3.25 |            885 |         84.90 |
| 10,096,066,651        |  1.25220 |              16 |                 2 |                       4 |               4.00 |           1064 |        101.00 |
| 12,630,874,972        |  1.25107 |              16 |                 2 |                       4 |               4.00 |           1404 |        133.00 |

It looks like we need about 160 bytes per locally owned active cell in 2d.

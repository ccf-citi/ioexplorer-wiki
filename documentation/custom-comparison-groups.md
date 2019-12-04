## Introduction

The Comparison Groups feature allows users to classify samples into groups with accuracy and precision for comparison in the Survival module. Using a specified syntax, outlined below, users can classify samples based on the existence and/or absence of mutations, expression levels, and clinical variable values.

#### Jumpstart Examples

Consider the following examples for an idea of how to use the Comparison Groups syntax to classify samples into custom groups for endpoint comparison.

###### Ex: Five groups of TMB
Samples with a TMB value between 0 and 2 will be classified in G1; those with a TMB value between 2 and 4 will be classified in G2, etc.
```
tmb [0, 2, 4, 8, 16, 32]
```

###### Ex: Metastatic Stage with two named categories
Samples with the stage `M0` will be assigned to the `m0` category. Samples with any of the stages `M1`, `M1A`, `M1B`, or `M1C` will be assigned to the `m1` category. Samples with any other stage value will not be assigned to a group and therefore will not be displayed on the plot.
```
m_stage {(m0, [M0]), (m1, [M1, M1A, M1B, M1C])}
```

###### Ex: Five groups of TP53 gene expression
The selected samples are automatically classified into evenly distributed groups based on gene expression values for the TP53 gene. The first group, `G0`, will consist of the first 20% of samples ranked by gene expression level in ascending order; The last group, `G4`, will consist of the last 20% of samples.
```
TP53 expression 5 groups
```

###### Ex: Any TP53 mutation
The selected samples are classified into two groups: those with a TP53 mutation and those without one.
```
TP53 any
```

###### Ex: All TP53 mutations
The selected samples are classified into five groups based on the type of its TP53 variant. The `Frame Shift` group includes `Frame_Shift_Ins` and `Frame_Shift_Ins` variants. The `In Frame` group includes `In_Frame_Ins` and `In_Frame_Del` variants. The `Missense` group includes the `Missense_Mutation` variant. The `Nonsense` group includes the `Nonsense_Mutation`. The `Splice Site` group includes the `Splice_Site` variant. If a samples does not have any TP53 variants, it is assigned to the `None` group.
```
TP53 all
```

###### Ex: Custom TP53 variant groups
The selected samples can be classified into custom groups based on the type of its TP53 variant. In this example, there are two custom groups: the `point` group includes samples with the `Missense_Mutation` and `Nonsense_Mutation` variants and the `indel` group includes the `In_Frame_Ins`, `In_Frame_Del`, `Frame_Shift_Ins`, `Frame_Shift_Del` variants. Any samples that do not have these names variants are classified into the `None` group.
```
TP53 {(point, [missense, nonsense]), (indel, [in frame, frame shift])}
```

###### Ex: Multi-Gene mutation
The selected samples are classified into groups based on the existence of variants in a list of genes.
```
(TP53, CDKN2A) any
```

###### Ex: Cartesian Product Groups
Users can classify samples into the Cartesian product of single-rule groups.
```
TP53 any X tmb [0, 2, 4, 8, 16, 32]
```
This rule leads to 10 distinct groups.

|                    | TMB G0            | TMB G1            | TMB G2            | TMB G3            | TMB G4            |
| ------------------ | ----------------  | ----------------  | ----------------  | ----------------  | ----------------  |
|  TP53 w/  variant  | TP53 w/  x TMB G0 | TP53 w/  x TMB G1 | TP53 w/  x TMB G2 | TP53 w/  x TMB G3 | TP53 w/  x TMB G4 |
|  TP53 w/o variant  | TP53 w/o x TMB G0 | TP53 w/o x TMB G1 | TP53 w/o x TMB G2 | TP53 w/o x TMB G3 | TP53 w/o x TMB G4 |

## Comparison Groups

Comparison Group types are split into three main categories.
 * Clinical Groups
 * Mutation Groups
 * Expression Groups

### Clinical Groups

#### Clinical Numeric Field Groups

Clinical Numeric Field groups are those based on a numeric-type clinical variable. Using a custom comparison group for a numeric-type clinical field gives the user the ability to define the exact intervals for which the selection of samples will be divided.

##### Ex: TMB with 5 groups
```
tmb [0, 2, 4, 8, 16, 32]
```
Samples with a TMB value between 0 and 2 will be classified in G1; those with a TMB value between 2 and 4 will be classified in G2, etc. Samples with a TMB value above 32 will not be assigned to a group and therefore will not be displayed on the plot.

#### Clinical String Field Groups

Clinical String Field groups are those based on a string-type clinical variable. Using a custom comparison group for a string-type clinical field gives the user the ability to drop certain values and combine others into named categories.

##### Ex: Cancer Type with 4 named categories
```
cancer type {(solid tumor, [Breast Cancer, Prostate Cancer]), (liquid tumor, [Leukemia])}
```
Samples with the cancer type `Breast Cancer` or `Prostate Cancer` will both be assigned to the `solid tumor` category. Samples with the cancer type `Leukemia` will be assigned to the `liquid tumor` category. Samples with any other cancer type value will not be assigned to a group and therefore will not be displayed on the plot.

#### Clinical Enum Field Groups

Clinical Enum Field groups are those based on a enum-type clinical variable. Using a custom comparison group for a enum-type clinical field gives the user the ability to drop certain values and combine others into named categories.

##### Ex: Metastatic Stage with 2 named categories
```
m_stage {(m0, [M0]), (m1, [M1, M1A, M1B, M1C])}
```
Samples with the stage `M0` will be assigned to the `m0` category. Samples with any of the stages `M1`, `M1A`, `M1B`, or `M1C` will be assigned to the `m1` category. Samples with any other stage value will not be assigned to a group and therefore will not be displayed on the plot.

The Clinical Enum Field Groups are essentially Clinical Enum Field Groups with one exception. If no named categories are given for an enum-type clinical variable, the system will include all of the possible types of the enum and create a named category for each one.

##### Ex: Metastatic Stage with no named categories
```
m_stage {()}
```
Samples with the stage `M0` will be assigned to the `M0` category; samples with the stage `M1` will be assigned to the `M1` category, etc. No samples are omitted.

### Mutation Groups

### Expression Groups

## Cartesian Product Groups

The Comparison Groups above classify samples into groups. However, a user may be interested in classifying samples into more than one group at a time. For example, a user may be interested in grouping samples with both the existence of a certain mutation, and its TMB value. This is possible by classifying samples into the [Cartesian product](https://en.wikipedia.org/wiki/Cartesian_product) of a set of rules.

##### Ex: Cartesian product rules (2D)
```
TP53 any X tmb [0, 2, 4, 8, 16, 32]
```
This rule leads to 10 distinct groups.

|                    | TMB G0            | TMB G1            | TMB G2            | TMB G3            | TMB G4            |
| ------------------ | ----------------  | ----------------  | ----------------  | ----------------  | ----------------  |
|  TP53 w/  variant  | TP53 w/  x TMB G0 | TP53 w/  x TMB G1 | TP53 w/  x TMB G2 | TP53 w/  x TMB G3 | TP53 w/  x TMB G4 |
|  TP53 w/o variant  | TP53 w/o x TMB G0 | TP53 w/o x TMB G1 | TP53 w/o x TMB G2 | TP53 w/o x TMB G3 | TP53 w/o x TMB G4 |

##### Ex: Cartesian product rules (3D)
```
TP53 any X PTEN expression 2 groups X tmb [0, 2, 4, 8, 16, 32]
```
This rule leads to 20 distinct groups.

|     | TMB G0 | TMB G1 | TMB G2 | TMB G3 | TMB G4 |
| --- | ------ | ------ | ------ | ------ | ------ |
|  TP53 w/  variant x PTEN G0 | TP53 w/  x PTEN G0 x TMB G0 | TP53 w/  x PTEN G0 x TMB G1 | TP53 w/  x PTEN G0 x TMB G2 | TP53 w/  x PTEN G0 x TMB G3 | TP53 w/  x PTEN G0 x TMB G4 |
|  TP53 w/  variant x PTEN G1 | TP53 w/  x PTEN G1 x TMB G0 | TP53 w/  x PTEN G1 x TMB G1 | TP53 w/  x PTEN G1 x TMB G2 | TP53 w/  x PTEN G1 x TMB G3 | TP53 w/  x PTEN G1 x TMB G4 |
|  TP53 w/o variant x PTEN G0 | TP53 w/o x PTEN G0 x TMB G0 | TP53 w/o x PTEN G0 x TMB G1 | TP53 w/o x PTEN G0 x TMB G2 | TP53 w/o x PTEN G0 x TMB G3 | TP53 w/o x PTEN G0 x TMB G4 |
|  TP53 w/o variant x PTEN G1 | TP53 w/o x PTEN G1 x TMB G0 | TP53 w/o x PTEN G1 x TMB G1 | TP53 w/o x PTEN G1 x TMB G2 | TP53 w/o x PTEN G1 x TMB G3 | TP53 w/o x PTEN G1 x TMB G4 |

### Limitations

There are some limits on the number (and type) of groups in the Cartesian product. The general maximum number of single-dimension group allowed is four (4). The maximum number of Mutation Groups allowed is two (2). Within a single-dimension group, there are no limit on the number of intervals/subgroups.

| Total # of Groups | # of Clinical / Expression Groups | # of Mutation Groups | Valid? | Example |
| ----------------- | ---------------------------------------- | -------------------- | ------ | ------- |
| >4 | * | * | no | |
| 4 | 4 | 0 | yes | `tmb [0, 4, 16, 64] X mean hed [5, 7, 9, 11] X TP53 expression 2 groups X PTEN expression 2 groups` |
| 4 | 3 | 1 | yes | `tmb [0, 4, 16, 64] X mean hed [5, 7, 9, 11] X TP53 expression 2 groups X PTEN any` |
| 4 | 2 | 2 | yes | `tmb [0, 4, 16, 64] X mean hed [5, 7, 9, 11] X TP53 any X PTEN expression 2 groups` |
| 4 | 1 | 3 | no | |
| 4 | 0 | 4 | no | |
| 3 | 3 | 0 | yes | `tmb [0, 4, 16, 64] X mean hed [5, 7, 9, 11] X TP53 expression 2 groups` |
| 3 | 2 | 1 | yes | `tmb [0, 4, 16, 64] X TP53 expression 2 groups X PTEN any` |
| 3 | 1 | 2 | yes | `tmb [0, 4, 16, 64] X TP53 any X PTEN any` |
| 3 | 0 | 3 | no | |
| 2 | 2 | 0 | yes | ` X tmb [0, 4, 16, 64]` |
| 2 | 1 | 1 | yes | `TP53 any X tmb [0, 4, 16, 64]` |
| 2 | 0 | 2 | yes | `TP53 any X CDKN2A any` |

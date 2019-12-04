The Comparison Groups feature allows users to classify samples into groups with accuracy and precision for comparison in the Survival module. Using a specified syntax, outlined below, users can classify samples based on the existence and/or absence of mutations, expression levels, and clinical variable values.

#### Jumpstart Examples

Consider the following examples for an idea of how to use the Comparison Groups syntax to classify samples into custom groups for endpoint comparison.

###### Ex: Five groups of TMB
Samples with a TMB value between 0 and 2 will be classified in G1; those with a TMB value between 2 and 4 will be classified in G2, etc.
```
tmb [0, 2, 4, 8, 16, 32]
```

###### Ex: Custom Stage Groups
Samples with Stage value of [`M0`] will be in group `m0`. Samples with the Stage value in [`M1`, `M1A`, `M1B`, `M1C`] will be in group `m1`. All samples with Stage values that do not match fall within these groups will be ignored.
```
m_stage {(m0, [M0]), (m1, [M1, M1A, M1B, M1C])}
```

###### Ex: Five groups of TP53 Gene Expression
The selected samples are automatically classified into evenly distributed groups based on gene expression values for the TP53 gene. The first group, `G0`, will consist of the first 20% of samples ranked by gene expression level in ascending order; The last group, `G4`, will consist of the last 20% of samples.
```
TP53 expression 5 groups
```

###### Ex: Any TP53 Mutation
The selected samples are classified into two groups: those with a TP53 mutation and those without one.
```
TP53 any
```

###### Ex: All TP53 Mutations
The selected samples are classified into five groups based on the type of its TP53 variant. The `Frame Shift` group includes `Frame_Shift_Ins` and `Frame_Shift_Ins` variants. The `In Frame` group includes `In_Frame_Ins` and `In_Frame_Del` variants. The `Missense` group includes the `Missense_Mutation` variant. The `Nonsense` group includes the `Nonsense_Mutation`. The `Splice Site` group includes the `Splice_Site` variant. If a samples does not have any TP53 variants, it is assigned to the `None` group.
```
TP53 all
```

###### Ex: Custom TP53 Variant Groups
The selected samples can be classified into custom groups based on the type of its TP53 variant. In this example, there are two custom groups: the `point` group includes samples with the `Missense_Mutation` and `Nonsense_Mutation` variants and the `indel` group includes the `In_Frame_Ins`, `In_Frame_Del`, `Frame_Shift_Ins`, `Frame_Shift_Del` variants. Any samples that do not have these names variants are classified into the `None` group.
```
TP53 {(point, [missense, nonsense]), (indel, [in frame, frame shift])}
```

###### Ex: Multi-Gene Variant Groups
The selected samples are classified into groups based on the existence of variants in a list of genes.
```
(TP53, CDKN2A) any
```

###### Ex: Cartesian Product Groups
Users can classify samples into the Cartesian product of single-rule groups.
```
TP53 any X tmb [0, 2, 4, 8, 16, 32]
```
This rule leads to 10 groups.

|                    | TMB G0 | TMB G1 | TMB G2 | TMB G3 | TMB G4 |
| ------------------ | ------ | ------ | ------ | ------ | ------ |
|  TP53 w/ variant   |        |        |        |        |        |
|  TP53 w/o variant  |        |        |        |        |        |

## Group Types

### Clinical Numeric Field Groups

### Clinical String Field Groups

### Clinical Enum Field Groups

### Mutation Groups

### Expression Groups

## Introduction

The AFL is a language intended to represent logical expressions for the selection of samples. In this language, there are filter rules and operators. Each rule, of which there are several categories and subtypes, specifies a subset of samples that should be used in statistical tests and visualizations. Rules can be combined and modulated by the operators for a functionally complete and thoroughly effective selection utility.

The AFL exhibits [functional completeness](https://en.wikipedia.org/wiki/Functional_completeness), meaning the available operators can be combined to produce all possible filter rule [truth tables](https://en.wikipedia.org/wiki/Truth_table).

### Jumpstart Examples

Consider the following examples for an idea of how to use the AFL to specify a selection of samples.

###### Ex: Select samples from male subjects that are above the age of 50.
```
sex in [MALE] and age > 50
```

###### Ex: Select samples with a tumor mutation burden (tmb) greater than or equal to 5 or some mutation of the TP53 gene.
```
tmb > 5 or TP53 any
```

###### Ex: Select samples with TAP1 expression in the bottom quartile or mean HLA evolutionary divergence in the bottom half.
```
TAP1 Q1 or hla_mean_evolutionary_diversity Q1-Q2
```
Read ahead for more details on Filter Rules and Operators.

## Filter Rules

There are three (3) categories of filter rules; each represents a different type of data.

### Clinical Rules

Clinical rules are used filter the sample selection based on fields that belong to the subject or sample. Examples of clinical fields include tumor mutational burden, immune cell counts, and HLA loci zygosity.

With the clinical rule category, there are several clinical rule types: Numeric, Quartile, and Categorical.

#### Clinical Numeric

The Clinical Numeric rule is used for numeric fields with a specific numeric operator. Take the `tmb` field as an example. Because it is a numeric field, one can select samples with `tmb` values based on comparison with a constant.

###### Ex: Valid Clinical Numeric Rules (tmb)
```
tmb > 10
tmb != 0
tmb <= 50
```

##### Clinical Quartile

The Clinical Quartile rule is used for numeric fields with a more general selection based on the distribution of that field. Within the Clinical Quartile rule set, there are two types of rules, each with a specific syntax. The first type is used to specify a single quartile; the second type allows a range of quartiles. Take the `age` field as an example.

###### Ex: Valid Clinical Quartile Rules (age)
```
age Q1
age Q4
age q2
age q3
age Q1-Q3
age Q3-Q4
age q1-q2
age q2-q4
```

##### Clinical Categorical

The Clinical Categorical rule is used for enumerated and string fields. To use the rule, the user will explicitly name the enum or string values that should be included in the sample selection. Take the `m_stage` field as an example.

###### Ex: Valid Clinical Categorical Rules (m_stage)
```
m_stage IN [M0]
m_stage In [MX]
m_stage in [M1A, M1B, M1C]
```

#### Mutation Rules

Mutation rules are used to select samples based on genetic variants, better known as mutations. These variants include frame shift indels, in frame indels, missense mutations, nonsense mutations and changes to the splice site among many others. A sample may have zero or more variants for a particular gene. Furthermore, this set of variants may be a diverse array of the variant types listed above.

Begin the rule with the HUGO symbol for the rule of interest. Read more about how gene symbols are handled [here](#Gene-Symbols).

To select a sample with a particular variant in a particular gene, use the Variant Set Mutation Rule type.

##### Variant Set

Use the keywords "include" and "exclude" along with a list of variant types to select samples. The "include" keyword indicates that the succeeding list of variants are the only variants that should be considered in the selection. The "exclude" keyword indicates that the succeeding list of variants should be ignored and all other variants should be considered in the selection.

Below is the list of default variants used for selection along with the valid aliases for each variant. All aliases are case-insensitive.

| Variant Type | Valid Aliases |
| --- | --- |
| Frame Shift (indel) | `frameshift` `frame shift` `frame_shift` |
| Frame Shift Ins     | `frameshiftins` `frame shift ins` `frame_shift_ins` |
| Frame Shift Del     | `frameshiftdel` `frame shift del` `frame_shift_del` |
| In Frame (indel)    | `inframe` `in frame` `in_frame` |
| In Frame Ins        | `inframeins` `in frame ins` `in_frame_ins` |
| In Frame Del        | `inframedel` `in frame del` `in_frame_del` |
| Missense Mutation   | `missense` `missense mutation` `missense_mutation` |
| Nonsense Mutation   | `nonsense` `nonsense mutation` `nonsense_mutation` |
| Splice Site         | `splicesite` `splice site` `splice_site` |


###### Ex: Valid Variant Set Mutation Rules
```
TP53 include [frame shift, nonsense]
BRCA1 Include [frame shift, splice site]
CDKN2A INCLUDE [frame Shift, missense, Nonsense]
PTEN exclude [frame shift, in frame]
BRAF Exclude [splice site]
TAP1 EXCLUDE [nonsense, missense, splice site]
```

##### Any Variant

For a more general method of selecting any variant types, use the `any` keyword.

###### Ex: Valid Variant Set Mutation Rules
```
TP53 any
BRCA1 ANY
CDKN2A ANY
PTEN any variants
BRAF Any Variants
TAP1 ANY VARIANTS
```

#### Expression Rules

Expression rules are used to select samples based on gene expression levels. Due to the high variability of expression values between genes, samples are selected by gene expression quartiles. The syntax of this rule matches the syntax of the [Clinical Quartile Rule](#Clinical-Quartile); both single quartile rules and quartile range rules are supported. Still, instead of specifying a clinical variable, the user specifies the HUGO symbol for the gene of interest.

###### Ex: Valid Expression Rules 
```
TP53 Q1
BRCA1 Q4
PTEN q2
BRAF q3
TAP1 Q1-Q2
KRAS Q3-Q4
CDKN2A q1-q3
BRCA2 q2-q4
```

### Operators

#### And Operator

#### Or Operator

#### Not Operator

## Additional Notes

### Clinical Variable Aliases

To refer to a clinical variable in the AFL, use any of the valid aliases for the clinical variable. These valid aliases can be found on the [Clinical Fields page](./clinical-fields).

[Clinical Fields page](clinical-fields)
[Clinical Fields page](/clinical-fields)
[Clinical Fields page](./clinical-fields)
[Clinical Fields page](../clinical-fields)
[Clinical Fields page](#clinical-fields)
[Clinical Fields page](#/clinical-fields)

### Gene Symbols

The AFL uses the HUGO symbol for human gene symbols. The rules pertinent to AFL users are listed below.
 - Human gene symbols are designated by **upper-case Latin letters** or by a combination of **upper-case letters** and **Arabic numerals**.
 - The initial character of the symbol should always be a letter. Subsequent characters may be other letters, or if necessary, Arabic numerals.

Though the HUGO symbol standard calls for upper-case letters, the IOExplorer system will recognize lower-case HUGO symbols.

For a more complete reference, see the Gene Symbol guidelines at [genenames.org](https://www.genenames.org/about/guidelines/#!/#tocAnchor-1-7)

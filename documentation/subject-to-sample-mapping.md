Due to the broad source of datasets, the IOExplorer system must allow for a number of Subject-Sample mapping types. This page describes the policies in place for each type of mapping.

In the current system, only one sample is used for analysis for each subject. Future releases will feature greater Subject-Sample selection flexibility and will allow the user to specify the Subject-Sample selection policy.

## One-to-One Mapping
In many datasets, there is only one sample collected for each subject. For these datasets, the mapping relationship remains as one-to-one. The samples selected correspond directly to a subject; all samples are included in the analyses.

|subject|sample|displayed?|
|---|---|---|
|subj01|samp01|yes|
|subj02|samp02|yes|
|subj03|samp03|yes|

## Treatment Status Field (Pre-On)
Some datasets will collect samples for patients before a treatment and during a treatment. For these datasets, the system will ignore the "ON treatment" samples and display only the "PRE treatment" samples. 

|subject|sample|Treatment Status|displayed?|
|---|---|---|---|
|subj01|samp01|PRE|yes|
|subj01|samp02|ON|no|
|subj02|samp03|PRE|yes|
|subj02|samp04|ON|no|
|subj03|samp05|NA|yes|

## Many-to-One Mapping
Some datasets have a many-to-one relationship between sample and subject without any reference to treatment status. For these datasets, the samples that map to a single subject are arbitrarily ordered so that only one sample will be used during analysis. This ordering exists in the database so the choice of sample is deterministic.

|subject|sample|displayed?|
|---|---|---|
|subj01|samp01|yes|
|subj01|samp02|no|
|subj01|samp03|no|
|subj02|samp04|yes|
|subj02|samp05|no|
|subj03|samp06|yes|

There are a number of relationships between the diverse data types in the system schema. This page describes these relationships and how they relate to the selection of samples for analysis.

Here is how the selection dogma breaks down.

A single study contains many subjects. A single subject is associated with at least one sample. This sample contains clinical data and is associated with number of different data types after downstream processing (DNA variants, RNA expression, etc.). Thus, from a single sample, the system can relate its demographic information, clinical data, genetic variants, RNA expression, and more.

Still, there is one important note about this grand association.

As noted above, a subject may have multiple associated samples. These samples are likely taken at different times, possibly related to treatment status. For a consistent result, the system has imposed a definitive mapping from each subject to a single sample. This way, with the same input, the system will produce the same output. Therefore, when a user selects a study in the StudySelect table, all of the associated subjects, samples and associated data, along the defined mapping, are added to the selection pool and used for analysis.

To learn more about this definitive mapping, read the [Subject-To-Sample Mapping page](subject-to-sample-mapping.md).

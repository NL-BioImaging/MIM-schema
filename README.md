# MIM: Multiomics and Imaging Metadata Schemas

**MIM (Multiomics and bioImaging Metadata)** is a collaborative, modular, [LinkML](https://linkml.io/linkml/intro/overview.html)-based metadata schema framework designed to harmonize experimental, sample, analytical, and instrument metadata across multiomics and bioimaging studies.

---

## The problem

Modern biomedical research increasingly combines high-resolution biological imaging with multiomics and single-cell assays. However, datasets generated across laboratories and modalities are frequently not **interoperable** and cannot be readily integrated, interpreted, or reused, slowing down discovery and limiting cross-modal analysis.

**At the heart of this interoperability crisis lies a metadata gap.** Reproducible experiments require structured, machine-actionable metadata, from study design, biosamples, perturbations, instrumentation to acquisition settings, and computational workflows. Existing standards solve critical pieces of this puzzle in isolation, yet leave gaps when studies span domains:

- **Domain-specific imaging and cytometry standards**—such as [**REMBI**](https://www.ebi.ac.uk/bioimage-archive/rembi-help-overview/) (REcommended Metadata for Biological Images, supported by the [BioImage Archive](https://www.ebi.ac.uk/bioimage-archive/rembi-model-reference/)) and **MIFlowCyt**, provide rich domain capture, but lack native abstractions for linking imaging or cytometry outputs with multiomics experiments.

- The [**ISA framework**](https://doi.org/10.1093/bioinformatics/btq415) (Investigation-Study-Assay) is a [general-purpose metadata format](https://isa-tools.org/format/specification.html) designed to standardize experimental data management. It facilitates bottom-up metadata curation, supports community-defined reporting standards, and streamlines submissions to public repositories. However, a key limitation of ISA is its lack of native support for imaging experiments.

## The solution
**MIM (`https://w3id.org/mim/`)** bridges multiomics and imaging metadata by separating **domain-agnostic experimental structure** from **specialized domain profiles**, authored in [**LinkML (YAML)**](https://linkml.io/linkml/intro/overview.html):

1. **JERM-Aligned Foundation (`schemas/foundation/`):** Establishes a shared core for projects, investigations, studies, assays, processes, protocols, samples, research assets, provenance, agents, institutions, and ontology-backed values.
2. **Modular Domain Profiles (`schemas/profiles/`):** Extends Foundation base classes (`MIMAssay`, `MIMProcess`, `MIMDataFile`, `MIMHardwareComponent`, `MIMReagentComponent`, `MIMTreatment`, `MIMPackage`) without duplicating core metadata entities.
3. **Hybrid Hierarchical Bundle Serialization (`MIMPackage`):** Embeds the experimental ownership hierarchy (`MIMProject` → `MIMInvestigation` → `MIMStudy` → `MIMAssay` → `MIMProcess`) while declaring reusable entities (`agents`, `institutions`, `protocols`, `samples`, `data_files`, `ontology_sources`) once in top-level registries referenced by identifier (`id`).
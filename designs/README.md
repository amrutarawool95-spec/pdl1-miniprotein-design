# Design outputs

No RFdiffusion/ProteinMPNN design PDBs are claimed yet. The current environment has no GPU or installed protein-design runtime, so adding fabricated coordinates here would make the project scientifically misleading.

Run notebooks 02–04 in Colab on a GPU. After a successful run, add only real outputs with:

- backbones/: RFdiffusion backbone PDBs
- sequences.csv: ProteinMPNN sequences and sampling metadata
- predictions/: ColabFold prediction PDBs
- design_manifest.csv: one row per design, including seeds and software versions

Every file should be traceable to a notebook run and a row in results/.

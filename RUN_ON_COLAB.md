# Run the real design on Google Colab

The repository now contains a real target artifact, but it does not contain fabricated binder PDBs. RFdiffusion and AlphaFold2-Multimer need a GPU runtime; use the links below from a phone browser.

## 1. Open the RFdiffusion notebook

[Open RFdiffusion v1.1.1 in Colab](https://colab.research.google.com/github/sokrypton/ColabDesign/blob/v1.1.1/rf/examples/diffusion.ipynb)

Set **Runtime → Change runtime type → T4 GPU**. Use the target file from this repository:

- [Download 4ZQK.pdb](https://raw.githubusercontent.com/amrutarawool95-spec/pdl1-miniprotein-design/main/target/4ZQK.pdb)
- Target chain: **A** (PD-L1)
- Binder length pilot: **50–80 residues**
- Pilot: **10 backbones**, not 100–200 yet
- Starting interface residues: **A56, A58, A66, A113, A115, A122, A123**

These are a conservative subset of the geometrically contacting PD-L1 residues. They are not all proven functional hotspots. The full contact map is in [target/interface_residues.csv](target/interface_residues.csv).

Record the notebook version, seed, target chain, hotspot string, binder length, and number of successful outputs before scaling up.

## 2. Design sequences

Use the ProteinMPNN step included in the RFdiffusion/ColabDesign workflow. Start with **8 sequences per accepted backbone**. Download:

- backbone PDBs
- designed sequences
- the notebook output or log showing sampling parameters

Do not keep only the best-looking structure; preserve the complete manifest.

## 3. Validate with ColabFold

[Open ColabFold AlphaFold2/Multimer in Colab](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb)

Run each binder against the PD-L1 chain and record:

- binder pLDDT
- interface PAE
- ipTM or interface confidence
- binder-only RMSD to the RFdiffusion backbone
- clashes and interface contacts

Use multiple seeds where the notebook supports them. The initial heuristic filters are pLDDT >= 80, interface PAE <= 10 Angstrom, binder-backbone RMSD <= 2 Angstrom, no major clashes, and overlap with the PD-1-facing surface.

## 4. Upload actual outputs

Add only outputs that came from the run:


designs/backbones/*.pdb
designs/predictions/*.pdb
designs/sequences.csv
results/design_manifest.csv
results/af2_metrics.csv

The repository is already set up for these paths. When you upload the files, include the seed and software version in the CSV. A passing computational filter is not experimental evidence of binding or checkpoint blockade.

## What I can do after upload

I can calculate the ranking table, cluster sequence diversity, compare each prediction with the PD-1-facing surface in 4ZQK, prepare the best-design figure, and update the report and CV bullet with the real counts.

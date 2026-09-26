# De novo PD-L1 miniprotein binder design

Computational design of compact protein binders targeting the PD-1-facing surface of human PD-L1.

> **Status:** Project scaffold. No designs, scores, affinity measurements, or experimental results are included yet.

## Scientific question

Can de novo miniprotein scaffolds be designed to occupy the PD-1-binding surface of PD-L1 and serve as computationally plausible checkpoint-blocking candidates?

This project uses the PD-1/PD-L1 complex in PDB **4ZQK** as the structural starting point. PD-L1 is a clinically validated and already drugged checkpoint target, so this project should be described as an exploration of an alternative compact binder modality—not as a solution to an undruggable target.

## Design pipeline

1. **Target preparation:** download 4ZQK, identify PD-1 and PD-L1 chains by sequence/annotation, and calculate the interface rather than assuming chain IDs or hotspot numbering.
2. **Backbone generation:** use RFdiffusion for 50–80 residue binder backbones conditioned on the PD-L1 surface and an explicitly documented hotspot set.
3. **Sequence design:** use ProteinMPNN to design multiple sequences per backbone. LigandMPNN is optional here because this is a protein–protein interface; its main advantage is explicit nonprotein context.
4. **Structure validation:** use ColabFold/AlphaFold2-Multimer with multiple seeds and record binder pLDDT, interface PAE, ipTM, binder-backbone RMSD, clashes, and interface recovery.
5. **Blocking analysis:** superpose predicted binder–PD-L1 complexes onto 4ZQK and quantify overlap with the PD-1-facing surface.
6. **Ranking:** combine structure consistency, interface confidence, clash checks, target-interface coverage, and sequence diversity. Keep all raw metrics.

## Suggested computational filters

These are heuristics, not proof of binding or blockade:

- Binder pLDDT >= 80
- Interface PAE <= 10 Angstrom
- Binder-only backbone RMSD to the designed backbone <= 2 Angstrom
- Reasonable interface confidence and no major steric clashes
- Measurable overlap with the PD-1-facing PD-L1 interface
- Sequence diversity after clustering

Thresholds and software versions must be recorded in the results files before ranking finalists.

## Repository structure


designs/ and large structure files should be added only after the first successful run. Avoid committing raw Colab caches or unreviewed generated structures.

```
notebooks/
  01_target_preparation.ipynb
  02_rfdiffusion_backbones.ipynb
  03_proteinmpnn_sequences.ipynb
  04_colabfold_validation.ipynb
target/
  README.md
  interface_residues.csv
results/
  design_manifest.csv
  af2_metrics.csv
  ranked_designs.csv
figures/
  README.md
report.md
```

## Literature rationale

- Muratspahic et al., **De novo design of miniproteins targeting GPCRs**, *Nature* (2026). [DOI](https://doi.org/10.1038/s41586-026-10656-8)
- Vazquez Torres et al., **De novo design of high-affinity binders of bioactive helical peptides**, *Nature* (2024). [PubMed](https://pubmed.ncbi.nlm.nih.gov/38109936/)
- Dauparas, Lee et al., **Atomic context-conditioned protein sequence design using LigandMPNN**, *Nature Methods* (2025). [DOI](https://doi.org/10.1038/s41592-025-02626-1)
- Krishna et al., **Generalized biomolecular modeling and design with RoseTTAFold All-Atom**, *Science* (2024). [DOI](https://doi.org/10.1126/science.adl2528)
- Zak et al., **Structure of the complex of human programmed death-1 and its ligand PD-L1**, PDB [4ZQK](https://www.rcsb.org/structure/4ZQK)

## Limitations

This is a computational study. Passing AlphaFold2 or geometric filters does not establish affinity, specificity, expression, stability, cell-surface activity, immune compatibility, or checkpoint blockade. RoseTTAFold All-Atom is not claimed as part of the current run unless it is actually executed and documented. PD-L1 glycosylation, membrane presentation, conformational dynamics, and off-target binding are not resolved by this scaffold alone.

## Reproducibility checklist

- [ ] Record target file checksum and chain mapping.
- [ ] Record RFdiffusion, ProteinMPNN, and ColabFold versions.
- [ ] Record seeds, lengths, sampling temperatures, and number of attempts.
- [ ] Preserve failed designs and filtering counts.
- [ ] Cluster final sequences and report diversity.
- [ ] Do not write a CV claim until the numbers are real and traceable to `results/`.

## Next steps

1. Run notebook 01 and populate `target/interface_residues.csv`.
2. Run a 10-backbone RFdiffusion smoke test.
3. Design sequences for successful backbones.
4. Validate a small pilot set before scaling up.
5. Add figures and a completed report only after the run produces real outputs.

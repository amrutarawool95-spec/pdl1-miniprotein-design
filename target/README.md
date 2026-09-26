# Target preparation

## Target

- PDB: 4ZQK
- Complex: human PD-1 / PD-L1
- Source: https://www.rcsb.org/structure/4ZQK

## Required checks

1. Download the mmCIF or PDB file.
2. Identify PD-1 and PD-L1 chains from sequence and RCSB annotation.
3. Calculate residue contacts using a documented heavy-atom distance cutoff.
4. Keep literature-supported hotspot annotations separate from geometric contacts.
5. Save the exact source file, checksum, chain mapping, and software version.

Do not assume that chain letters or residue numbering in an external tutorial match the downloaded structure. The notebook should generate the final contact list used by RFdiffusion.

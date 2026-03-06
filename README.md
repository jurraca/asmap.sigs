Repository containing ASmap file attestations.

The [asmap-data](https://github.com/bitcoin-core/asmap-data) repository contains ASmaps for use with Bitcoin Core. This repository contains attestations on those files.

### Process

Creating an ASmap for use with Bitcoin Core starts with a "collaborative run" ([example](https://github.com/bitcoin-core/asmap-data/issues/42)), where each participant start [Kartograf](https://github.com/asmap/kartograf) at the same Unix timestamp.

If a majority of participants arrive at the same output ASmap, that output is a candidate for use with Bitcoin Core. An ASmap must be encoded for use with Core, using the [asmap-tool](https://github.com/bitcoin/bitcoin/tree/master/contrib/asmap) utility. 

Upon submission to the [asmap-data](https://github.com/bitcoin-core/asmap-data) repository, participants should recreate the hashes for these ASmaps, and sign them with their PGP key.

### Commands

From a `bitcoin` directory with the bitcoin-core source tree, with a `final_result.txt` ASmap output
- To encode an _unfilled_ ASmap:
  - `python contrib/asmap/asmap-tool.py encode final_result.txt output_asmap_unfilled.dat`
- To encode a _filled_ ASmap:
  - `python contrib/asmap/asmap-tool.py encode --fill final_result.txt output_asmap_filled.dat`

### Directory Structure

- `<run epoch>/<signer>`: each ASmap from a collaborative run is run at a specific epoch (Unix timestamp), which serves to identify a given run.
  - `SHA256SUMS`: hashes of the `filled` and `unfilled` encoded ASmap 
  - `SHA256SUMS.asc`: detached PGP signature over the `output.SHA256SUMS` file
- `builder-keys/<signer>.gpg`: signer keys


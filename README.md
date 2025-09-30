[![Website](https://img.shields.io/badge/sqr--105-lsst.io-brightgreen.svg)](https://sqr-105.lsst.io)
[![CI](https://github.com/lsst-sqre/sqr-105/actions/workflows/ci.yaml/badge.svg)](https://github.com/lsst-sqre/sqr-105/actions/workflows/ci.yaml)

# Adding VOParquet serializer to TAP Service (qserv-kafka)

## SQR-105

This document describes the implementation of VOParquet output format support in the qserv-kafka bridge and our TAP Service. 
VOParquet is a Virtual Observatory standard that embeds VOTable metadata within Parquet files. 
The implementation addresses the challenges of adapting Parquet's column-oriented architecture to a scenario where we want to efficiently stream rows from a database to a GCS bucket, while limiting the memory footprint.
The solution employs a batched processing approach, achieving near-comparable performance to the existing binary2 VOTable encoder while reducing output sizes by approximately 40%. 
In this document we document the increased memory usage in the form of spikes due to the accumulation of metadata required by the Parquet format. The implementation successfully handles queries up to QServ's memory limits and maintains compatibility with VO tools such as TOPCAT. 
We not the tradeoffs including increased implementation complexity and higher memory requirements compared to the streaming VOTable encoder as well as the advantages of this format which is the smaller result file-sizes.

**Links:**

- Publication URL: https://sqr-105.lsst.io
- Alternative editions: https://sqr-105.lsst.io/v
- GitHub repository: https://github.com/lsst-sqre/sqr-105
- Build system: https://github.com/lsst-sqre/sqr-105/actions/


## Build this technical note

You can clone this repository and build the technote locally if your system has Python 3.11 or later:

```sh
git clone https://github.com/lsst-sqre/sqr-105
cd sqr-105
make init
make html
```

Repeat the `make html` command to rebuild the technote after making changes.
If you need to delete any intermediate files for a clean build, run `make clean`.

The built technote is located at `_build/html/index.html`.

## Publishing changes to the web

This technote is published to https://sqr-105.lsst.io whenever you push changes to the `main` branch on GitHub.
When you push changes to a another branch, a preview of the technote is published to https://sqr-105.lsst.io/v.

## Editing this technical note

The main content of this technote is in `index.md` (a Markdown file parsed as [CommonMark/MyST](https://myst-parser.readthedocs.io/en/latest/index.html)).
Metadata and configuration is in the `technote.toml` file.
For guidance on creating content and information about specifying metadata and configuration, see the Documenteer documentation: https://documenteer.lsst.io/technotes.

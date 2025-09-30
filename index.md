# Adding VOParquet serializer to TAP Service (qserv-kafka)

```{abstract}
This document describes the implementation of VOParquet output format support in the qserv-kafka bridge and our TAP Service. 
VOParquet is a Virtual Observatory standard that embeds VOTable metadata within Parquet files. 
The implementation addresses the challenges of adapting Parquet's column-oriented architecture to a scenario where we want to efficiently stream rows from a database to a GCS bucket, while limiting the memory footprint.
The solution employs a batched processing approach, achieving near-comparable performance to the existing binary2 VOTable encoder while reducing output sizes by approximately 40%. 
In this document we document the increased memory usage in the form of spikes due to the accumulation of metadata required by the Parquet format. The implementation successfully handles queries up to QServ's memory limits and maintains compatibility with VO tools such as TOPCAT. 
We not the tradeoffs including increased implementation complexity and higher memory requirements compared to the streaming VOTable encoder as well as the advantages of this format which is the smaller result file-sizes.
```

## Add content here

See the [Documenteer documentation](https://documenteer.lsst.io/technotes/index.html) for tips on how to write and configure your new technote.

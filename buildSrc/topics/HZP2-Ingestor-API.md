# HZP2 - Ingestor API

As mentioned in _HZP1_, the Ingestor can be implemented in some different ways,
to ensure stable interoperability with other components, we define an API based on gRPC
to which all ingestor implementations must adhere.

## Concepts

The two main concept in the realtime data ingestion are snapshotting and streaming.

### Snapshotting

1. Include incremental snapshot
2. Include blocking snapshot
3. Table dependency resolving out of the box
4. Possibly parallelization snapshotting

### Streaming

1. Default dbz streaming functionality
2. Monitoring api


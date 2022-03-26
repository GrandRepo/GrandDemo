# Grand
---
Grand is a system for automatically finding logic bugs in GDBs. The core idea of Grand is to construct semantically equivalent databases for multiple GDBs, and then compare the 
results of a Gremlin query on these databases. If the returned results of a query on multiple GDBs are different, the likely cause is a bug in these GDBs. 
We evaluate Grand on six widely-used GDBs, i.e., [Neo4j](https://neo4j.com), [JanusGraph](https://janusgraph.org), [TinkerGraph](https://github.com/tinkerpop/blueprints/wiki/tinkergraph),
 [Arcadedb](https://arcadedb.com/), [Orientdb](https://www.orientdb.org/), and [HugeGraph](https://hugegraph.github.io/hugegraph-doc/).

## Guidelines
---
To prove Grand is available, we take two GDBs, JanusGraph and TinkerGraph, as example to show how to use Grand locally.

### Setting GDBs
- Download JanusGraph server from its [official website](https://github.com/JanusGraph/janusgraph/releases), replace `conf\gremlin-server\gremlin-server.yaml` with
`janus\gremlin-server.yaml` we offered.
- Download TinkerGraph server from its [official website](https://tinkerpop.apache.org/download.html), replace `conf\gremlin-server.yaml` with
  `tinker\gremlin-server.yaml` we offered.
- Start the JanusGraph server and TinkerGraph server respectively using command `./bin/gremlin-server.sh start` under the root path of each gdb server.

### Runing Grand
Using command `java -jar gdbtesting.jar QueryDepth VerMaxNum EdgeMaxNum EdgeLabelNum VerLabelNum QueryNum` to start Grand, the parameters represents for
- `QueryDepth`, the max length of the query we generated, e.g., 8.
- `VerMaxNum`, the maximum number of the Vertex in the generated graph, e.g. 500.
- `EdgeMaxNum`, the maximum number of the Edge in the generated graph, e.g., 500.
- `EdgeLabelNum`, the maximum number of the edge label in the generated graph, e.g., 20.
- `VerLabelNum`, the maximum number of the vertex label in the generated graph, e.g., 20.
- `QueryNum`, the number of query generated in a test round, e.g., 200.

### Checking Results
Result files are stored under path `log-1`, including:
- `schema.txt`, records the schema information of generated graph.
- `xxx-graphdata.txt`, records the graph data information of each gdb.
- `xxx-Map.txt`, records the mapping information of vertexes and edges of each gdb.
- `xxx-1.txt`, records the result of each query.
- `check-1.txt`, records the result comparison of gdbs.
- `result-1.txt`, records the serial number of queries that have different results from gdbs.

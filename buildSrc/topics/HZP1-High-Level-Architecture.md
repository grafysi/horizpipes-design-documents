# HZP1 - High-level architecture

Horizpipes is a realtime integration system designed specific for streaming
data from EHR databases of healthcare providers to analytics graph databases
of Grafysi.

The following figure depicts components of Horizpipes and the flow of data
through them.

```plantuml
```
{src = "puml/High_Level_Architecture.puml"}

## Ingestor

The ingestor abstract the process of interacting with source databases 
to get transaction logs in real-time and format these logs into some standard 
structures called `change_records`. As the name implied, each `change_record` 
provides details about change event, i.e. `INSERT`, `UPDATE`or
`DELETE`, of a database row.

The method used to track row-level changes in source database is change-data-capture
(CDC). The CDC system continuously fetches or subscribes, depending on 
each RDBMS provider, for transaction logs and formats the logs into `change_records`
so that the formated records are as _RDBMS-agnostics_ as possible.

There are some options listed below for implementation of Ingestor based on CDC method, but for
now, all of these options are designed around the Debezium platform which provides
many out-of-the-box connectors to track row-level changes in almost all mainstream
RDBMS.

1. Running debezium connector as kafka connect task, where each table is ingested
to a dedicated kafka topic (default behaviour).
   - Pros: easy to implement as it is default behaviour provided by Debezium platform.
   - Cons: The event time ordering is not guaranteed between inter-related records from
   different tables. Introduce many difficulties for downstream systems to process data
   in parallel.
2. Running debezium connector as kafka connect tasks, where __all table__ are 
ingested into one kafka topic.
    - Pros: time-order of all change events are guaranteed as they are ingested
   in one topic. Give downstream system more freedom for parallelizing.
    - Cons: Need to customize behaviour of debezium, schema registry 
   (we use apicurio), etc.
3. Running debezium engine in custom runtime.
    - Pros: Costly to implement reliable custom solution.
    - Cons: Independent of kafka, might be flexible and cheaper in deployment.

For now, we adopt the option 2 for implementation of ingestor.

## SourcePort

```plantuml
```
{src = puml/SourcePort_Dataflow.puml}

## Processor

```plantuml
```
{src = "puml/Processor_Architecture.puml"}


## SinkPort

```plantuml
```
{src = "puml/SinkPort_Architecture.puml"}

## Loader

```plantuml
```
{src = "puml/Loader_Architecture.puml"}


























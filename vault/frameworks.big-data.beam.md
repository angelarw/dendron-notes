---
id: 270884d9-210b-42e0-88a3-7193738d3233
title: Apache Beam
desc: ''
updated: 1614537039727
created: 1604607282027
---

## Overview

* [2018 PyCon talk - Streaming data processing pipelines with Apache Beam in Python](https://www.youtube.com/watch?v=I1JUtoDHFcg)


![](/assets/images/2020-11-05-15-17-16.png)

- **Beam** is a collection of SDKs for streaming processing pipeline
    - name come from 'Batch' + 'strEAM'
    - https://github.com/apache/beam
    - ![](/assets/images/2020-11-05-15-22-21.png)
    - ![](/assets/images/2020-11-05-15-23-36.png)
        - Streaming + accumulation: built-in fucntionality for handle late packets  
    - Beam Pipeline is a DAG graph 
    - **Bounded** (batch) vs **Unbounded** (streaming, with windows)
    - **PCollection** == data elements 
        - iterable collection
        - immutable -readonly                
    - **PTransform** == nodes in the graph 
        ```python
        records = (p 
            | 'Read from PubSub' >> beam.io.ReadStringsFromPubSub(topic=..., id_label='MESSAGE_ID')
            | 'Parse JSON to dict' >>  beam.Map(lambda e: json.load(e))

        # branch 1
        records | beam.ParDo(AddTimstampToDict())
                    | beam.WindowInto(window.SlidingWindows(..))
                    | beam.ParDo(AddKeyToDict())
                    | beam.GroupByKey()
                    | beam.Pardo(CountAverages())
                    | beam.io.WriteToBigQuery(...)

        # branch 2          
        records | beam.io.WriteToBigQuery(...)
        ```

- **Cloud Dataflow** - managed service 





### On AWS 

* Workshop on using Beam with Kinesis Flink: https://beam-streaming-analytics.workshop.aws/en/beam-on-kda.html

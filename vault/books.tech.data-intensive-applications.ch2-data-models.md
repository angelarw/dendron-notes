---
id: 45199987-a515-40d0-8bc8-c447503f21b1
title: Ch02 - Data Models and Query Languages
desc: ''
updated: 1614536991037
created: 1604342702043
---

# Chapter 2 - data models and query languages 

## Relational vs document 
Roots of RDMS: business data processing - mainframe in the 1960s and ’70s. 
-  transaction processing (entering sales or banking transactions, airline reservations, stock-keeping in warehouses) 
- batch processing (customer invoicing, payroll, reporting )

### Object-relational mismatch
- For a data structure like a résumé, which is mostly a self-contained document, a JSON representation can be quite appropriate 
- Document: better locality 
- one-to-many relationships imply tree structure- captured well by JSON
- Many-to one relationships - e.g. normalizing city of people 
    - not easy with doc data base 
    - Emulate join in application code rather than database
- Many to many relationships
- Not a new debate:
    - Hierarchical model
    - Network model

#### RDMS vs document databases today
- Document: schema flexibility, performance due to locality, sometimes closer to data structures used by application 
- Which data model leads to simpler application code? 
    - Document: If the data in your application has a document-like structure (i.e., a tree of one-to- many relationships, where typically the entire tree is loaded at once 
    - highly interconnected data : document is awkward, relational acceptable, graph most natural
- Schema
    - Document databases - schema-on-read - like dynamic type checking 
        -  advantageous if the items in the collection don’t all have the same structure for some reason 
    - Relational - schema-on-write. -  like static/compile time type checking
        -  most relational database systems execute the ALTER TABLE statement in a few milliseconds except MySQL 
- Data locality for queries
    - Document is usually stored as single continuous string. So if often eed access to entire doc, performance advantage
    - Not limited to document db:
        -   locality property in a relational model 
            - Spanner: rows nested in parent
            - Oracle: multi-table index cluster table
            - Bigtable, Cassandra and HBase : column family 

## Query languages
- declarative query language: 
    - hides implementation details - Improve perf w/o requiring query changes 
    - lend themselves to parallel execution 
    - Example: css
    - MapReduce query in MongoDB
        -  Neither declarative nor fully imperative
        -  Alternative: Mongo Aggregation pipeline: declarative - looks a lot like SQL 
        -  "a NoSQL system may find itself accidentally reinventing SQL, albeit in disguise. " 
## Graph data models
- Great for many-to-many relationships 
- Can be emulated with recursive queries in Relational. But awkward
- Type: 
    - Property graph - Neo4J
    - Triple-store model
        -  Resource Description Framework (RDF) - designed for semantic web - never took off 
        -  Subject - predicate - object 
        -  Predicate used for both property and edges
            
            ```
            - prefix : \<urn:example:\>.
                _:lucy     a       :Person.
                _:lucy     :name   "Lucy".
                _:lucy     :bornIn _:idaho
            ```
- Query language:
    - Declarative:
        -  SparQL - for triple stores using the RDF data model
        -  Datalog - predicate(subject, object) - build rules small steps at a time 
        -  Cypher - neo4j 
    - Imperative: 
        -  Gremlin

## Summary
- Historically, data started out being represented as one big tree (the hierarchical model), but that wasn’t good for representing many-to-many relationships, so the relational model was invented to solve that problem 
- Recently noSQL:
    - Document - when relationships across docs is rare
    - Graph  - when anything is related to anything 
		

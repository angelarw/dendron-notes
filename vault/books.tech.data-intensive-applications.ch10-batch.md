---
id: b0ec61b7-70af-48f2-8c44-df56afab8f5d
title: Ch10 - Batch processing
desc: ''
updated: 1614537039718
created: 1605153348300
---


# The Unix Philosophy
- Make each program do one thing well
- output of every program to become the input to another unkonwn program
- friendly to experimentation 
- Use tools in preference to unskilled help (prefer automation)

example: linux `sort` util: do one thing really well, but only powerful when combined with other tools

- Batch Processing with Unix Tools
    - **Chain of commands** versus custom program 
        - Sorting vs in-memory aggregation: example - count the most frequent URLs 
            - if large amount of data, sorting can make efficient use of disks 
                - Mergesort has sequential access patterns that perform well on disks
            - small number of uniq values: in memory hash table may works great

- **A uniform interface**
    - interface is **file**: actual file, socket, stdin, stdout, device driver, etc. 
- Separation of logic and wiring
    - defaulting to stdin and stdout allows loose coupling and program doesn’t know or care where input comes from or output going
- Transparency and experimentation
    - input immutable, can repeatly run
    - can inspect intermediate results 
    - piping output to file allows checkpointing progress

# MapReduce

Lots of parallel with Unix: 
- 



---
id: 48575b62-61b9-4ee8-be31-67c48966a2fe
title: Cloud
desc: ''
updated: 1614537039736
created: 1605882339173
---

- [Using HPC and ML on AWS to understand climate change](https://www.allthingsdistributed.com/2020/11/science-of-climate-change.html) 
    - Maxar Technologies - weather prediction models 
        - c5n.18xlarge + EFA networking adapter 
        - 14TB FSx for Lustre with progressive file layout (PFL) across the 12 object storage targets (OSTs).
            ![](/assets/images/2020-11-20-11-21-07.png)
    - cloud efficiencies:
        - A typical large-scale cloud provider achieves ~65 % server utilization rates versus 15% on-premises (source - [Data Center Efficiency Assessment](https://www.nrdc.org/sites/default/files/data-center-efficiency-assessment-IP.pdf)). which means when companies move to the cloud  they typically provision fewer than ¼ of the servers than they would on-premises.
        - A typical on-premises data center is 29% less efficient in their use of power compared to a typical large-scale cloud provider 

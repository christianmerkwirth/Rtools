-   [What is R?](#what-is-r)
-   [What aren’t you telling me about
    R?](#what-arent-you-telling-me-about-r)
-   [Secrets to using R in
    production](#secrets-to-using-r-in-production)
-   [Speeding up your R code](#speeding-up-your-r-code)
-   [Why cloud ?](#why-cloud)
-   [Easy to parallelize](#easy-to-parallelize)
-   [Frameworks when it’s not easy to
    parallelize](#frameworks-when-its-not-easy-to-parallelize)
-   [What is Apache Spark?](#what-is-apache-spark)
-   [R and Spark: Sparklyr](#r-and-spark-sparklyr)
-   [Things to note](#things-to-note)
-   [Getting code into the cloud](#getting-code-into-the-cloud)
-   [Getting data into the cloud](#getting-data-into-the-cloud)
-   [Packages to make R cloud-ready](#packages-to-make-r-cloud-ready)
-   [Google Cloud Platform](#google-cloud-platform)
-   [Dataproc](#dataproc)
-   [Big Query](#big-query)
-   [Data Flow](#data-flow)
-   [GCP specific packages](#gcp-specific-packages)
-   [Starting and Managing GCE
    instances](#starting-and-managing-gce-instances)
-   [Managing data on Google
    Datascore](#managing-data-on-google-datascore)
-   [Sparklyr & Dataproc](#sparklyr-dataproc)
-   [Machine Learning with SparklyR](#machine-learning-with-sparklyr)
-   [Analyzing NYC Taxi Data Set with Sparklyr and
    BigQuery](#analyzing-nyc-taxi-data-set-with-sparklyr-and-bigquery)
-   [BigRQuery](#bigrquery)
-   [BigQueryR](#bigqueryr)
-   [Cloud ML](#cloud-ml)
-   [Best practices - Data](#best-practices---data)
-   [Best practices - Costs](#best-practices---costs)
-   [Questions](#questions)

What is R?
----------

-   Widely used data science software
-   Used by millions of data scientists, statisticians and analysts
-   Most powerful statistical programming language
-   Flexible, extensible and comprehensive for productivity
-   Creates beautiful and unique data visualizations
-   As seen in New York Times or The Economist
-   Thriving open-source community
-   Leading edge of Statistics research

What aren’t you telling me about R?
-----------------------------------

-   R is single-threaded
-   R is an in-memory application
-   R is difficult to learn initially.
-   And yet, major companies use R for production data science on large
    databases.
-   Examples:
    -   \[blog.revolutionanalytics.com/applications/\]

Secrets to using R in production
--------------------------------

-   Don’t use R alone. – Know what it’s good for! (And what it’s not
    good for.) – Use R as part of a production stack
-   Use modern R workflows – Be able to hire great data scientists
-   Use R in conjunction with parallel/distributed data & compute
    architectures\*

Speeding up your R code
-----------------------

-   On a single machine
    -   Vectorize
    -   Use *data.table*
-   Move to the cloud and parallelize
    -   Easy to parallelize
    -   Hard to parallelize

Why cloud ?
-----------

-   Get machines, storage and network as a service
    -   From a single, persisent VM to a fully managed cluster
    -   Let others care for maintenance, update, repairs
    -   Virtually unlimited resources on demand
    -   Pay only what you use
-   Platforms:
    -   [Google Cloud Platform (GCP)](https://cloud.google.com/)
    -   [Amazon AWS](https://aws.amazon.com/)
    -   [Microsoft Azure](https://azure.microsoft.com/)

Easy to parallelize
-------------------

-   A problem is easy to speedup when:
    -   Calculating similar things many times – Iterations in a loop,
        chunks of data, …
    -   Calculations are independent of each other
    -   Each calculation takes a decent amount of time
-   Just run multiple calculations in parallel on several machines
    -   Easy to do with say 5-10 shards
    -   With a 100+ shards, there are problems of load balancing, tasks
        dying etc.
    -   Big cloud comapnies spend immense amount of engineering time to
        develop their cluster operating system

Frameworks when it’s not easy to parallelize
--------------------------------------------

-   Use a framework
    -   Flow processing frameworks (e.g. Map-Reduce, Flume)
    -   Query processing frameworks (e.g. BigQuery)
-   Some frameworks can do both
-   Apache Spark becomes increasingly popular as a general purpose
    framework

What is Apache Spark?
---------------------

-   Distributed cluster processing engine.
-   Successor to Hadoop
-   Store and analyze massive volumes in a robust, scalable cluster
-   In-memory engine 100x faster than map-reduce
-   Highly extensible, with machine-learning capabilities
-   Supports Scala, Java, Python, R ...
-   *Managed* cloud services available – GCP Dataproc
    -   Azure Databricks
    -   AWS EMR

R and Spark: Sparklyr
---------------------

-   sparklyr:
    -   R interface to Spark – open-source R package from RStudio
-   Move data between R and Spark
-   Keeps *References* to Spark Data Frames – Familiar R operations,
    including dplyr syntax – Computations offloaded to Spark cluster,
    and deferred until needed
-   CPU/RAM/Disk consumed in cluster, not by R
-   Interfaces to Spark ML algorithms

Things to note
--------------

-   All of the computation take place in the Spark cluster –
    Computations are delayed until you need results – Behind the scenes,
    Spark SQL statements are being written for you
-   None of the data comes back to R – Until you call collect, when it
    becomes a tibble – It’s only at this point you have to worry about
    data size
-   Use ordinary dplyr syntax to interact with data in Spark cluster

Getting code into the cloud
---------------------------

-   [Github](github.comn) or [Google
    Source](https://cloud.google.com/source-repositories/) repos keep
    versioned code persistently
-   Docker images used to spawn nodes – Default: rocker/tidyverse:latest
    – Lots of R packages pre-installed
-   But this cross-validation also needs: – xgboost, e1071
-   Easy fix: build your own docker image
    -   write a Dockerfile that builds on an already existing Rocker
        image
    -   add packages and applications
-   Build Docker images in the cloud
    -   120 min free build time daily in GCP

Getting data into the cloud
---------------------------

-   Speed hierarchy
    -   Superfast: In cloud, same region & zone
    -   Fast: In cloud, different region or zone
    -   Okay: Between different cloud platforms
    -   Slow: Between cloud and your local machine
-   Collect and keep the data in the cloud
    -   Manage data downloads from within a VM instance
    -   Check whether to keep data on persistent data storage

Packages to make R cloud-ready
------------------------------

-   General
    -   Tidyverse
    -   sparklyr
    -   foreach, future
-   Platform specific packages
    -   Cloudyr: GCP, AWS
    -   Azure

Google Cloud Platform
---------------------

Dataproc
--------

-   Managed Spark cluster of user-specified size
-   All installations done automatically
-   Setup and turndown within minutes
-   Pay for machines (master + workers) plus some cluster fee
-   Attach SSDs on demand
-   Connectors to Bigquery and Datastore for fast data import
-   R preinstalled on master and worker nodes
-   Works smoothly with sparklyr

Big Query
---------

-   Sifting through terybytes of data
-   Using SQL like syntax
-   Super fast
-   Limited expressiveness
-   Fully managed, no need to specify cluster size
-   Pay for data volume processed
-   Ideal solution for preprocessing and condensing

Data Flow
---------

-   GCP Dataflow (aka Flume)
-   Most complicated option
    -   Needs significant amount Java recoding for every new problem
    -   Run FlumeJava with embedded Java-based R interpreter Renyin
-   Might give highest computational throughput at given cost level
-   <https://medium.com/google-cloud/cloud-dataflow-can-autoscale-r-programs-for-massively-parallel-data-processing-492b57bd732d>

GCP specific packages
---------------------

-   Management of VMs
    -   googleComputeEngineR:
    -   googleAuthR:
-   Managed frameworks
    -   Spark: [sparklyr]()
    -   Big Query I: [bigRQuery]()
    -   Big Query II:
        [bigQueryR](https://cran.r-project.org/web/packages/bigQueryR/vignettes/bigQueryR.html)
    -   Big Table:
    -   Cloud ML: \[cloudml\]

Starting and Managing GCE instances
-----------------------------------

Managing data on Google Datascore
---------------------------------

Sparklyr & Dataproc
-------------------

Machine Learning with SparklyR
------------------------------

-   SparklyR provides R interfaces to Spark’s distributed machine
    learning algorithms (MLlib)
-   Computations happing in the Spark cluster, not in R

Analyzing NYC Taxi Data Set with Sparklyr and BigQuery
------------------------------------------------------

<https://www.r-bloggers.com/new-york-city-taxi-limousine-commission-tlc-trip-data-analysis-using-sparklyr-and-google-bigquery/>

BigRQuery
---------

<https://cloud.google.com/blog/big-data/2017/04/google-cloud-platform-for-data-scientists-using-r-with-google-bigquery>

BigQueryR
---------

<https://cran.r-project.org/web/packages/bigQueryR/vignettes/bigQueryR.html>

Cloud ML
--------

<https://tensorflow.rstudio.com/tools/cloudml/articles/getting_started.html>

Best practices - Data
---------------------

-   Keep data close
    -   Speed cascade (same rack, same interlink, same datacenter, same
        zone, same region, out of cloud)
-   If possible, keep data in the cloud
    -   Costs vs speed of accesss
    -   Remember to store on persistent storage
-   Manage data from within the cloud
    -   Use a GCE instance in the cloud as your console to move data
-   Retrieve only reasonable small datasets out of the cloud
    -   Condensed, manageable sized results
    -   Generate visualizations and reports in cloud

Best practices - Costs
----------------------

-   On most platforms, you pay
    -   Compute resources by minute
        -   Preemptive or spot instances can be much cheaper
    -   Storage by size \* duration
    -   Queries by processed data volume
-   Make sure
    -   To check pricing, promos and free tier
    -   To develop your approach on a smaller (but not too small) subset
        of data
    -   Allocate only those resourced needed
    -   Take down VMs, clusters after processing
    -   Check for not longer needed storage
    -   Set proper quotas
    -   Preemptive or spot resources can be much cheaper

Questions
---------

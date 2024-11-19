SLO service level objective

MTTR mean time to repair

# Implementaion
## Implementing SLO's

Service level objectives(SLOs) specify a target level for the reliability of your service. Because SLOs are key to making data-driven decisions about reliability, they're at the core of SRE practices.

It's (SLO) the target level of reliability for the service's customers. Above this threshold, almost all users should be happy. Below this threshold, users are likely to start complaining or to stop using the service.

If you want 100% of relibility it's not a reasonable goal
There is a long chain b/w user and sre so anything can be wrong.

canbe go from 99% to 99.9% to 99.9% but brings only marginal changes to the customers. not a lot of changes to them. but increase the cost of doing it marginally

IF you want to maintain you can never update or improve the service. the no one source of outages is change: pushing new features, applying security patches, deplying new hardware and scaling up to meet customers demand will impact that 100% target.

100% SLO means you only have time to be reactive.


## What to Measure: Using SLI's

SLI = Service Level Indicators

General recommendation is treating the SLI as the ratio of 2 numbers.

* Number of successful HTTP requests / Total HTTP requests(success rate)
* Number of gRPC calls that completed successfully in < 100ms / total gRPC requests
* No of serach results that used teh entire corpus / total nubmer of search results, including those that degraded gracefully
* No of "stock check count" requests from product searches that used stock data fresher than 10min / total no of stock check requests
* No of "good user minutes" according to some extended list of criteria for that metric / total no of user minutes


#### Figuring out SLI's


* Choose one application for which you want tot define SLOs. If your product comprises many applications, you can add those later.

* Decide clearly who the "users" are in the situation. These are the people whose happiness you are optimizing.

* Consider the common ways your users interact with your system-common tasks and critical activites.

* Draw a high-level architecture diagram of your system; show the key components, the request flow, the data flow, and the critical dependencies. Group these components into categories listed in the following section (there maybe some overlap and ambiguity; user your intuition and don't let perfect be the enemy of the good).

#### Types of componets

abstracting your system into a few common types of components is teh easiest way to get started with setting SLI's

Request-driven

    The user creates some type of event and expects a response. For example, this could be an HTTP service where the user interacts with the browser of an API for a mobile application.

Pipeline

    A system that takes records as input, mutates them, and places the o/p somewhere else. This might be a simple process that runs on a single instance in real time, or a multistage batch process that takes many hours.

        A sytem taht periodically reads data from a relational database and writes it into a distribute hash table for optimized serving

        A video processing service that converts video from one format to another

        A system that reads in log files from many sources to generate reports

        A monitoring system that pulls metrics from remote servers and generates time series and alerts

Storage

    A system that accepts data(eg bytes, records, files, videos) and makes it available to be retrieved at a later data.
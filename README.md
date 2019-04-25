# adr-rackspace
________________________________________________
V1

Context: 

  Mailtrust is an email hosting company. It employs support techs who search the logs to troubleshoot issues for the customers. 
  The support techs do not have login access to the servers so they have to escalate the ticket to their engineers.
  As the company is more and more growing, the process of logging into each server is too time consuming for their engineers.
  Besides, the server's performance is highly impacted during a simultaneous query from engineers.

Scenario of performance:

  Source: 
  The support tech escalate a ticket to the engineer
  Stimulus: 
  The engineer is performing queries.
  Artefact: 
  Server MTX002 (mail server)
  Environment: 
  The mail server is currently operational, another engineer is performing queries on the server
  Response: 
  The server returns the log after a long duration
  Measure: 
  Time of response between the server and the system
  

________________________________________________
V2

Context:

The company released a log search tool using a single machine MySQL version. 
The engineers are no longer involved in the process as the support techs are able to use this new tool. 
However, MySQL inserts rapidly become the bottleneck of the process.
Indeed, indexing each entry as it is inserted becomes slow as the amount of data received is too important. 
Besides, there are no recovering system for the log system in case of a system failure.

Scenario of availability

  Source: 
  Log search tool
  Stimulus: 
  Support techs perform search query
  Artefact: 
  Server MTX109 (mail server)
  Environment:
  The server is currently operational
  Response:
  The system returns random errors
  Measure:
  Number of missing log data
 
________________________________________________
V3

Context:

As the company is growing exponentialy, the previous solution of breaking data into merge tables based on time eventually broke down with a combination of load and operational issues. 
The matter is to find the best solution of log processing that will answer to the scalability and reliability concerns. 
The company built a new log processing system using Hadoop, Lucene and Solr, mainly for its scalability. 
The solution seems to be suiting its needs as the only problems, the company are facing to this day, are their own bugs.

Scenario of reliability

  Source: 
  The engineer queries the server for statistics concerning number of logins
  Stimulus: 
  Nightly MapReduce jobs collect data about number of logins
  Artefact: 
  Server MTX167 (mail server)
  Environment: 
  The server is currently operationnal
  Response: 
  The system returns the number of logins
  Measure: 
  Time of response of the system

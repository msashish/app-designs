## Problem

    You have large incoming data in the form of files, and tables. Design a Spark application that performs tokenisation
    of incoming data with following features:
    
        1) Should be configuration driven 
        2) Can be plugged/un-plugged into existing data ingestion/processing pipelines 
        3) Should be restartable (considering large incoming data)
        4) Should have necessary quality checks
        
       Tokenisation definition: Tokenisation replaces sensitive data with unique values (tokens) that are unrelated to 
       the original value in any algorithmic sense thereby satisfying the PCI-DSS guidance.
       
       Assumption:  A restful encryption service is available to tokenise upto 10k subjects in a single request.
       
       Expectation: Candidate to show high level design, different components involved and class diagram 

## Considerations and discussions

    1) How to process data in batches ?
    2) Are Checkpoints essential ?
    3) What all quality checks are essential and why ?

## Solution
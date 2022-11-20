## Problem

    You are working for a stockbroking house and you have trading terminals across the country where stocks are 
    bought / sold between 9.15 AM to 3.30 PM. Consider millions of transactions every 15 mins.
    
    Your requirement is to design an Application on hadoop that processes transactions and produces a cumulative 
    buy sell report with below characteristics:
    
        1) Report should be refreshed every 15 mins
        2) Report should show correct total buy, total sell and net value for that 15 mins period

    Initial Assumption: Ingestion team is able to bring millions of records to your Data Lake in appx 15 minutes. You 
    keep getting new file every 15 minutes
    

## Considerations and discussions

    1) Is there any flaw (issues) in achieving the requirement ?
    2) Modify initial assumption and discuss on different components involved.
    3) Handling late events, and duplicates ?



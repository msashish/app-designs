## Problem
    
    You are working for a payment bank where millions of transactions occur on customer's credit card and savings 
    account every day from Bank's website/App.
     
    Your requirement is to design an application that performs following:
     
     1) Review transaction for fraud and approve/reject at real-time (response in ms)
        To make a decision, there are many rules, one of which needs past 100 transactions on the Account
     
     2) Process transactions at near real-time for adjusting/modifying user statistics/profile (response in minutes)
     
     3) Provide ability for analytical/exploratory processing of data
     
     Your bank has been investing heavily on Hadoop clusters and would like you consider one or more hadoop clusters.

    Expectation: To come up with high level design, different components involved.

## Considerations and discussions

    1) Client side component 
    2) Hadoop component to use for real-time activities
    3) Hadoop component to use near-real-time processing
    4) Hadoop component to use for exploratory activities
    5) Storage considerations
    6) Any caching (local, remote) component that will be needed ?
    7) Where will fraud rules reside ?

## Design Overview
    <img src="..click-stream-design.png">]

 
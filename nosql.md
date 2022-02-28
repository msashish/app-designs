## Youtube link Introduction to NoSQL • Martin Fowler • GOTO 2012

    - SQL's impedence mismatch problem
        We assemble structures of objects in memory often interms of cohesive whole of things and then strip out into bits for storing in different tables.
        If we consider elements and data in a UI page then one simple logical structure will be stored differently. Its hence mismatch in how things are and how they have to be stored. Two different way of looking at things.
    - Why Relational DB dominated ?
        Because they had become integration mechanism. Many people integrated different applications through SQL DB. 
    - SQL was designed to work on one large big system and not on multiple small systems (boxes)
        Since running SQL DB on multiple small systems is difficult, it inspired noSQL such as Google's BigTable.
        NoSQL was just a Twitter hashtag to organise a meetup. Accidently it became a movement.

    - Definition
        Cannot be defined but we can list characteristics:
            not relational
            cluster friendly (can run in multiple small machines)
            open source
            schema less
        Four catagories
            Document DB         - MongoDB, CouchDB, GCP FireStore/DataStore
            Wide Column family  - BigTable, HBASE, Cassandra
            Graph DB            - Neo4j
            key value           - redis, riak, GCP memorystore
    Key value, wide Column and Document DB are aggregate oriented database. Meaning they aggregate a lot of attributes thereby representing them as one structure. 
    Aggregate orientation fits naturally for storing data in large clusters
    Aggregate orientation is advantage if we push/pull data using same aggregate. Its a disadvantage if we want to slice and dice (like sql queries)

    - Transaction handling (transactions == atomic updates)
        Graph DB - ACID like Relational DB
        Aggregate oriented DB - As per DDD, aggregate update is atomic i.e ACID within aggregates

    - CAP Theorem
        When you get a network partition (i.e distributed system) then you get either consistency OR availability but not both.

    - Drivers for noSQL DB ?
        Large scale data (that needs to be stored in distributed system)
         
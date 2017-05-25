# facedb
blockchain database with face recognition hashes, times, and GPS locations

Purpose

In Scope
  Public domain
  decentralized
  open source
  three tables only
    facehashversion
      hashid
      hashcode
      hashversion
    face
      faceid
      face hash
      hash name

Not In Scope


Design
  tables
  
It may make the most sense to have one table in each thin blockchain.  If users want to add columns, they can copy a blockchain, add their features, and be responsible for launching, promoting and maintaining it themselves.  Universal and competing APIs can interact with multiple "table" blockchains and choose the best of available tables for their purpose. 

Table blockchain selection factor will be API compatibility, availibility, nodes, ownership, cost, columns, data quality, userbase, FK interoperability.  worldwide datasets will have duplication and compete between public domain, corporate owned, and government owned
    hashversion
      desc:
        has details of face recognition hash algorithum used.
        1-10 records used as FK to face table.
        unique composite key is hashcode + hashversion.
      columns:
        hashcodeversionid, smallint, PK
        hashcode, string FK to external industry standard?
        hashversion, string.  Version of hashcode
        
      
    hash
      desc:
        a unique list of hashes with no times or GPS tags.  Hashes can be multiple versions.
        depending on hash used, there may also be a confidence % column.
        The idea would be to reduce duplication if helpful.  If log entry duplication can't be avoided, then this table should be flattened with the log table.
        examples of hashes could be security camera or facebook style face recognition, it could be deduping sensor data like a runner's footsteps, or a vendor profile for companies who deal with 500 + vendors.
        narrow table of unique face hash + hashid.
        PK is hashid
        unique composite key is hashdata + hashcodeversionid
        hashid is something like a bigint as a FK to log table
      columns:
        hashid, PK, bigint or more
        hashdata 
        hashcodeversionid
      
    gpslog
      desc:
        log the hash captured, time, and geolocation into the publich blockchain.
      columns:
        logtime
        hashid
        
    interactionlogs
      desc:
        in additoin to the gps log, there are many non-gps applications for putting hashes into a blockchain.  In a vendor scenario, you could use Dun and bradstreet numbers instead of hashes, log your own company DUNS umber, and your vendor's DUNS, the time, and 1-3 narrow interaction flags like dollar buckets, sentiment, transaction type, accept vs. reject, etc.
      
      

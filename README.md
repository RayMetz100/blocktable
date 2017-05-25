# blocktable
Overview
A blocktable is a tiny/thin simple database table replicated in it's own individual blockchain.  The blocktable in itself is not an application, but an API to store, retrieve, and search data.  Typically they will have 2-5 low byte columns.  

Background
Like value tokens, blocktables will be coded by multiple teams, public and corporate, have multiple languages and APIs.  Their usefulness will be their simplicity.  

Scenarios
External applications will interact with one or more of these blocktables and join to internal non-block tables as well.  Applications will be written in a flexible manner so that if a better block table becomes more useful later, the application can switch if they want.  A user application might use eight blocktables run by different external orgs and 20 internal tables.  If an application has a need for a public blocktable, but one doesn't exist yet, they can launch a new external or internal blocktable and use it in their application. They can choose any business or security model they wish and promote it as they see fit.  Some teams may specialize in creating and maintaining blocktables only, while other teams may specialize in using blocktables in their applications.

A company like Microsoft could reuse their blocktable code base and deploy 20 of them with similar APIs, then use many of them in a single application.  Each blocktable would be it's own entity with no dependencies though.  Decentralized, and shared with competitors.

Tech notes
It may make the most sense to have one table in each thin blockchain.  If users want to add columns, they can copy a blockchain, add their features, and be responsible for launching, promoting and maintaining it themselves.  Universal and competing APIs can interact with multiple "table" blockchains and choose the best of available tables for their purpose. 

Table blockchain selection factor will be API compatibility, availibility, nodes, ownership, cost, columns, data quality, userbase, FK interoperability.  worldwide datasets will have duplication and compete between public domain, corporate owned, and government owned

blocktable application example, security face recognition logging (or dashcam license plate logging):

Purpose
  Database with face recognition hashes, times, and GPS locations

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
      
      

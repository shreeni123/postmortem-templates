> Template from: Betsy Beyer, Chris Jones, Jennifer Petoff, and Niall Richard Murphy. [“Site Reliability Engineering.”](https://landing.google.com/sre/book/chapters/postmortem.html).

# Root Cause Analysis for AES EDI - JIRA Issue AESEDI-53447 (incident #143)

### Date
2020-06-25
### Authors
Shree Iyer
### Status
Complete, resolved
### Summary
The customer data was not sent from AES EDI. The investigation showed that the file with the data was sent, but it did not get processed due to an issue with the AES CIS service
### Impact
486,000 records were affected. The EDS to CIS monitoring service was also affected.
### Root Causes
A file with large number of records being sent at the same time while running the patching script caused a wreck in data processing. The problem with AES CIS service led to missing records.
### Trigger
A large number of files did not get processess
### Resolution
Reloading the AES CIS monitoring service allowed us to identify the missed records that could not be discovered automatically.
### Detection
The customer created a Jira Ticket to alert us on this failure. Please refer JIRA Issue: (AESEDI-53447)
## Action Items
| Action Item | Type | Owner | Bug |
| ----------- | ---- | ----- | --- |
| Create a monitoring policy to detect missing records | prevent | SI | **DONE** |
| Monitor the data ingesters and processors (ETL) | prevent | SI | (Jira Issue No: AESCIS-38263)**TODO** |
## Lessons Learned
Need to add more monitoring plugins to monitor this critical part of the infrastructure

## Timeline
2020-06-25 (*all times EDT*)

| Time  | Description |
| ----- | ----------- |
| 11:56 | Discovered missing files |
| 12:00 | Restarted the AES CIS monitoring module |
| 12:15 | Started data processing of records |
| 13:00 | Completed data processing of all 486,000 records |

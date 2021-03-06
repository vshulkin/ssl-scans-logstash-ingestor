# ssl-scans-logstash-ingestor
Runs SSL Labs or SSlyze tests against domains, outputs data into logstash with proper formatting.

# Work in progress
Initial push is just the logstash configuration.  A script is used that can be used in bulk scanning or continous integration systems.  Script will be posted soon.

# SSL Labs
The logstash configuration will parse SSL labs results and create a new record for each endpoint tested. 

To see it in action:   

```
curl "https://api.ssllabs.com/api/v2/analyze?host=www.ssllabs.com&all=done" | curl -XPOST https://logstashhost:PORT --data-binary @-
```

# SSLyze

The logstash configuration also supports parsing SSlyze scans, some light sanitation is required before posting.  The main script handles this much better, however the following example command will give you a general idea.

To see it in action:  

```
sslyze --regular --json_out=- www.google.com | sed -e 's/OpenSslVersionEnum.*/"&"/' | sed -e 's/, "/",/g' | curl -XPOST https://logstashhost:PORT --data-binary @-
```
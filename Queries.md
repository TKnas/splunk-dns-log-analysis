**1. Search for DNS Evetns**
  * Launch the Splunk interface and navigate to the search bar.
  * Use the following query to pull all DNS-related events:

```spl
index=* sourcetype="DNS"
```

Note: "DNS" is the sourcetype name you assigned when uploading the data.

**2. Extract Relevant Fields**
  * Identify important fields in DNS logs, such as source IP, destination IP, domain name, query type, response code, and more.
  * You can use a regex to search for common DNS-related keywords in the raw event data. For example:

```spl
| regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```

Full example query:
```spl
index=* sourcetype=dns_sample | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```
This helps isolate DNS-specific information from the raw logs for easier analysis.

**3. Identity Threat or Unusual Pattern**
  * Analyze DNS activity to spot any unusual or suspicious patterns.
  *	Example query to highlight such events:

```spl
index=* sourcetype="DNS" | stats count by full_qualified_domain_name
```
This query counts the number of occurrences for each domain, helping to identify domains with abnormal or excessive query activity.

**4. Search for the top DNS sources**
  * Find the unusual number of queries from each domain name and source IP 
  * Example query to highlight such events:

```spl
index=* sourcetype="DNS" | top full_qualified_domain_name, src_ip
```

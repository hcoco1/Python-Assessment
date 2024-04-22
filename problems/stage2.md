##### Navigation

[Back to Home 🏠](../README.md) | [Back to Stage: Identification ](stage1.md)  |  [Next: Stage: Preservation](stage3.md)

## Stage  Analysis

Once the devices involved have been identified and isolated, and the data has been duplicated and stored securely, digital forensic investigators use various techniques to extract relevant data and examine it, searching for clues or evidence that points to wrongdoing (Gonzalez, 2022).

With a clear understanding of the file's location, permissions, and integrity status, the process to edit the config.conf file was undertaken. The Vim text editor was used to append the configuration lines (Figure 2. [admin]: AliceAdmin1 & IvanAdmin2) to enable proper logging functionality within the Splunk server. 


```bash
fstack@:/opt/splunk/etc/system/local$ vim config.conf
[inputs]
 - Windows logs
 - Firewall logs
 - Jira logs
 - Software engineering logs
 - IPS logs
 - IDS logs
 - WAF logs

[viewers]
 - Emily
 - Neel
 - James
 - Riley
 - Sara

# Configuration lines added
[admin]             
   ─ AliceAdmin1
   ─ IvanAdmin2
```
<small>**Fig.4** Command to edit the `config.conf` file (vim)</small> 

Following the editing process, another round of MD5 hash verification confirmed the integrity of the modified config.conf file, validating that the modifications were successfully applied without unintended alterations (Figure 5).

```bash
fstack@:/opt/splunk/etc/system/local$ md5sum config.conf 
46dfaf406b12c9d1ca9b293660c2939b  config.conf
```
<small>**Fig.5** Command to hash the `config.conf` file (md5sum)</small>

##### Navigation

[Back to Home 🏠](../README.md) | [Back to Stage: Identification ](stage1.md)  |  [Next: Stage: Preservation](stage3.md)
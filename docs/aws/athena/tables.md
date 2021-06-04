# Creating and maintaining Athena tables


    show create table table
    describe table
    show tblproperties db.table


# Describing tables

    SHOW CREATE TABLE <database>.<table_name>;
    

## Cloudfront logs

    
    CREATE EXTERNAL TABLE `<database>.cloudfront_logs`(
      `date` string COMMENT '', 
      `time` string COMMENT '', 
      `x_edge_location` string COMMENT '', 
      `sc_bytes` string COMMENT '', 
      `c_ip` string COMMENT '', 
      `cs_method` string COMMENT '', 
      `cs_host` string COMMENT '', 
      `cs_uri_stem` string COMMENT '', 
      `sc_status` string COMMENT '', 
      `cs_referer` string COMMENT '', 
      `cs_user_agent` string COMMENT '', 
      `cs_uri_query` string COMMENT '', 
      `cs_cookie` string COMMENT '', 
      `x_edge_result_type` string COMMENT '', 
      `x_edge_request_id` string COMMENT '', 
      `x_host_header` string COMMENT '', 
      `cs_protocol` string COMMENT '', 
      `cs_bytes` string COMMENT '', 
      `time_taken` string COMMENT '', 
      `x_forwarded_for` string COMMENT '', 
      `ssl_protocol` string COMMENT '', 
      `ssl_cipher` string COMMENT '', 
      `x_edge_response_result_type` string COMMENT '', 
      `cs_protocol_version` string COMMENT '', 
      `fle_status` string COMMENT '', 
      `fle_encrypted_fields` string COMMENT '', 
      `c_port` string COMMENT '', 
      `time_to_first_byte` string COMMENT '', 
      `x_edge_detailed_result_type` string COMMENT '', 
      `sc_content_type` string COMMENT '', 
      `sc_content_len` string COMMENT '', 
      `sc_range_start` string COMMENT '', 
      `sc_range_end` string COMMENT '')
    ROW FORMAT SERDE 
      'org.apache.hadoop.hive.serde2.RegexSerDe' 
    WITH SERDEPROPERTIES ( 
      'input.regex'='\'([^ ]*) ([^ ]*) \\\\[(.*?)\\\\] ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) \\\\\\\"([^ ]*) ([^ ]*) (- |[^ ]*)\\\\\\\" (-|[0-9]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) (\\\"[^\\\"]*\\\") ([^ ]*)(?: ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*))?.*$\' ') 
    STORED AS INPUTFORMAT 
      'org.apache.hadoop.mapred.TextInputFormat' 
    OUTPUTFORMAT 
      'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
    LOCATION
      's3://<bucket_path>'
    TBLPROPERTIES (
      'has_encrypted_data'='false', 
      'transient_lastDdlTime'='1602752772')
  
  
## S3 website logs

    SHOW CREATE TABLE s3_logs;
  
  
    CREATE EXTERNAL TABLE `s3_logs`(
      `bucketowner` string COMMENT '', 
      `bucket` string COMMENT '', 
      `requestdatetime` string COMMENT '', 
      `remoteip` string COMMENT '', 
      `requester` string COMMENT '', 
      `requestid` string COMMENT '', 
      `operation` string COMMENT '', 
      `key` string COMMENT '', 
      `requesturi_operation` string COMMENT '', 
      `requesturi_key` string COMMENT '', 
      `requesturi_httpprotoversion` string COMMENT '', 
      `httpstatus` string COMMENT '', 
      `errorcode` string COMMENT '', 
      `bytessent` bigint COMMENT '', 
      `objectsize` bigint COMMENT '', 
      `totaltime` string COMMENT '', 
      `turnaroundtime` string COMMENT '', 
      `referrer` string COMMENT '', 
      `useragent` string COMMENT '', 
      `versionid` string COMMENT '', 
      `hostid` string COMMENT '', 
      `sigv` string COMMENT '', 
      `ciphersuite` string COMMENT '', 
      `authtype` string COMMENT '', 
      `endpoint` string COMMENT '', 
      `tlsversion` string COMMENT '')
    ROW FORMAT SERDE 
      'org.apache.hadoop.hive.serde2.RegexSerDe' 
    WITH SERDEPROPERTIES ( 
      'input.regex'='([^ ]*) ([^ ]*) \\[(.*?)\\] ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) \\\"([^ ]*) ([^ ]*) (- |[^ ]*)\\\" (-|[0-9]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) (\"[^\"]*\") ([^ ]*)(?: ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*))?.*$') 
    STORED AS INPUTFORMAT 
      'org.apache.hadoop.mapred.TextInputFormat' 
    OUTPUTFORMAT 
      'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
    LOCATION
      's3://<s3-website-logs-bucket-path>'
    TBLPROPERTIES (
      'transient_lastDdlTime'='1602747483')

  

    describe s3_website_logs

    bucketowner         	string              	                    
    bucket              	string              	                    
    requestdatetime     	string              	                    
    remoteip            	string              	                    
    requester           	string              	                    
    requestid           	string              	                    
    operation           	string              	                    
    key                 	string              	                    
    requesturi_operation	string              	                    
    requesturi_key      	string              	                    
    requesturi_httpprotoversion	string              	                    
    httpstatus          	string              	                    
    errorcode           	string              	                    
    bytessent           	bigint              	                    
    objectsize          	bigint              	                    
    totaltime           	string              	                    
    turnaroundtime      	string              	                    
    referrer            	string              	                    
    useragent           	string              	                    
    versionid           	string              	                    
    hostid              	string              	                    
    sigv                	string              	                    
    ciphersuite         	string              	                    
    authtype            	string              	                    
    endpoint            	string              	                    
    tlsversion          	string       

  
For the first table above

    show tblproperties db.table

    transient_lastDdlTime	1602752772
    EXTERNAL	TRUE
    has_encrypted_data	false

  
In sidebar, 3 dots, Show Properties, has:

- table name
- database name
- create time 
- has encrypted data

The create time matches the transient_lastDdlTime above





# MSCK

not always recommended

    msck repair table db.table

  
  

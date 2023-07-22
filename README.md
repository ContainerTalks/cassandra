# Run Cassandra as Container

## Cassandra Default Keyspaces

- `system_traces` -   
- system_schema  
- system_auth  
- system  
- system_distributed

## Connecting to Cassandra Container

```bash
docker exec -it cassandra-one bash # Container Name

root@cassandra-one:/# cqlsh # Now you are in container with root user

Connected to Universe at 127.0.0.1:9042. # Universe is the CASSANDRA_CLUSTER_NAME 
[cqlsh 5.0.1 | Cassandra 3.9 | CQL spec 3.4.2 | Native protocol v4]
Use HELP for help.
cqlsh> desc keyspaces; # Describe or List the Keyspaces

system_traces  system_schema  system_auth  system  system_distributed

cqlsh> use system_traces ;
cqlsh:system_traces> desc tables; # List the tables in keyspace system_traces

events  sessions
```

## Ports Used
    - 7000 # Intra-node communication
    - 7001 # TLS intra-node communication
    - 7199 # JMX
    - 9042 # CQL
    - 9142 # CQL SSL

## JVM Options:

-Xloggc:/var/log/cassandra/gc.log, -ea, 
-XX:+UseThreadPriorities, 
-XX:ThreadPriorityPolicy=42, 
-XX:+HeapDumpOnOutOfMemoryError, 
-Xss256k, 
-XX:StringTableSize=1000003, 
-XX:+AlwaysPreTouch, 
-XX:-UseBiasedLocking, 
-XX:+UseTLAB, 
-XX:+ResizeTLAB, 
-XX:+PerfDisableSharedMem, 
-Djava.net.preferIPv4Stack=true, 
-XX:+UseParNewGC, 
-XX:+UseConcMarkSweepGC, 
-XX:+CMSParallelRemarkEnabled, 
-XX:SurvivorRatio=8, 
-XX:MaxTenuringThreshold=1, 
-XX:CMSInitiatingOccupancyFraction=75, 
-XX:+UseCMSInitiatingOccupancyOnly, 
-XX:CMSWaitDuration=10000, 
-XX:+CMSParallelInitialMarkEnabled, 
-XX:+CMSEdenChunksRecordAlways, 
-XX:+CMSClassUnloadingEnabled, 
-XX:+PrintGCDetails, 
-XX:+PrintGCDateStamps, 
-XX:+PrintHeapAtGC, 
-XX:+PrintTenuringDistribution, 
-XX:+PrintGCApplicationStoppedTime, 
-XX:+PrintPromotionFailure, 
-XX:+UseGCLogFileRotation, 
-XX:NumberOfGCLogFiles=10, 
-XX:GCLogFileSize=10M, 
-Xms992M, 
-Xmx992M, 
-Xmn248M, 
-XX:CompileCommandFile=/etc/cassandra/hotspot_compiler, 
-javaagent:/usr/share/cassandra/lib/jamm-0.3.0.jar, 
-Dcassandra.jmx.local.port=7199, 
-Dcom.sun.management.jmxremote.authenticate=false, 
-Dcom.sun.management.jmxremote.password.file=/etc/cassandra/jmxremote.password, 
-Djava.library.path=/usr/share/cassandra/lib/sigar-bin, 
-Dcassandra.libjemalloc=/usr/lib/x86_64-linux-gnu/libjemalloc.so.1, 
-Dlogback.configurationFile=logback.xml, 
-Dcassandra.logdir=/var/log/cassandra, 
-Dcassandra.storagedir=/var/lib/cassandra, 
-Dcassandra-foreground=yes]

## Configuration:

allocate_tokens_for_keyspace=null; 
authenticator=AllowAllAuthenticator; 
authorizer=AllowAllAuthorizer; 
auto_bootstrap=true; 
auto_snapshot=true; 
batch_size_fail_threshold_in_kb=50; 
batch_size_warn_threshold_in_kb=5; 
batchlog_replay_throttle_in_kb=1024; 
broadcast_address=192.168.48.2; 
broadcast_rpc_address=192.168.48.2; 
buffer_pool_use_heap_if_exhausted=true; 
cas_contention_timeout_in_ms=1000; 
cdc_enabled=false; 
cdc_free_space_check_interval_ms=250; 
cdc_raw_directory=null; 
cdc_total_space_in_mb=null; 
client_encryption_options=<REDACTED>; 
cluster_name=SolarSystem; 
column_index_cache_size_in_kb=2; 
column_index_size_in_kb=64; 
commit_failure_policy=stop; 
commitlog_compression=null; 
commitlog_directory=/var/lib/cassandra/commitlog; commitlog_max_compression_buffers_in_pool=3; 
commitlog_periodic_queue_size=-1; 
commitlog_segment_size_in_mb=32; 
commitlog_sync=periodic; 
commitlog_sync_batch_window_in_ms=null; 
commitlog_sync_period_in_ms=10000; 
commitlog_total_space_in_mb=null; 
compaction_large_partition_warning_threshold_mb=100; 
compaction_throughput_mb_per_sec=16; 
concurrent_compactors=null; 
concurrent_counter_writes=32; 
concurrent_materialized_view_writes=32; 
concurrent_reads=32; 
concurrent_replicates=null; 
concurrent_writes=32; 
counter_cache_keys_to_save=2147483647; 
counter_cache_save_period=7200; 
counter_cache_size_in_mb=null; 
counter_write_request_timeout_in_ms=5000; 
credentials_cache_max_entries=1000; 
credentials_update_interval_in_ms=-1; 
credentials_validity_in_ms=2000; 
cross_node_timeout=false; 
data_file_directories=[Ljava.lang.String;@2928854b; disk_access_mode=auto; disk_failure_policy=stop; 
disk_optimization_estimate_percentile=0.95; 
disk_optimization_page_cross_chance=0.1; 
disk_optimization_strategy=ssd; 
dynamic_snitch=true; 
dynamic_snitch_badness_threshold=0.1; 
dynamic_snitch_reset_interval_in_ms=600000; 
dynamic_snitch_update_interval_in_ms=100; 
enable_scripted_user_defined_functions=false; 
enable_user_defined_functions=false; 
enable_user_defined_functions_threads=true; 
encryption_options=null; 
endpoint_snitch=GossipingPropertyFileSnitch; 
file_cache_size_in_mb=null; 
gc_log_threshold_in_ms=200; 
gc_warn_threshold_in_ms=1000; 
hinted_handoff_disabled_datacenters=[]; 
hinted_handoff_enabled=true; 
hinted_handoff_throttle_in_kb=1024; 
hints_compression=null; 
hints_directory=null; 
hints_flush_period_in_ms=10000; 
incremental_backups=false; 
index_interval=null; 
index_summary_capacity_in_mb=null; 
index_summary_resize_interval_in_minutes=60; 
initial_token=null; 
inter_dc_stream_throughput_outbound_megabits_per_sec=200; 
inter_dc_tcp_nodelay=false; 
internode_authenticator=null; 
internode_compression=dc; 
internode_recv_buff_size_in_bytes=null; 
internode_send_buff_size_in_bytes=null; 
key_cache_keys_to_save=2147483647; 
key_cache_save_period=14400; 
key_cache_size_in_mb=null; 
listen_address=192.168.48.2; 
listen_interface=null; 
listen_interface_prefer_ipv6=false; 
listen_on_broadcast_address=false; 
max_hint_window_in_ms=10800000; 
max_hints_delivery_threads=2; 
max_hints_file_size_in_mb=128; 
max_mutation_size_in_kb=null; 
max_streaming_retries=3; 
max_value_size_in_mb=256; 
memtable_allocation_type=heap_buffers; 
memtable_cleanup_threshold=null; 
memtable_flush_writers=1; 
memtable_heap_space_in_mb=null; 
memtable_offheap_space_in_mb=null; 
min_free_space_per_drive_in_mb=50; 
native_transport_max_concurrent_connections=-1; native_transport_max_concurrent_connections_per_ip=-1; native_transport_max_frame_size_in_mb=256; 
native_transport_max_threads=128; 
native_transport_port=9042; 
native_transport_port_ssl=null; 
num_tokens=128; otc_coalescing_strategy=TIMEHORIZON; 
otc_coalescing_window_us=200; 
partitioner=org.apache.cassandra.dht.Murmur3Partitioner; 
permissions_cache_max_entries=1000; 
permissions_update_interval_in_ms=-1; 
permissions_validity_in_ms=2000; 
phi_convict_threshold=8.0; 
prepared_statements_cache_size_mb=null; 
range_request_timeout_in_ms=10000; 
read_request_timeout_in_ms=5000; 
request_scheduler=org.apache.cassandra.scheduler.NoScheduler; 
request_scheduler_id=null; 
request_scheduler_options=null; 
request_timeout_in_ms=10000; 
role_manager=CassandraRoleManager; roles_cache_max_entries=1000; roles_update_interval_in_ms=-1; 
roles_validity_in_ms=2000; 
row_cache_class_name=org.apache.cassandra.cache.OHCProvider; row_cache_keys_to_save=2147483647; 
row_cache_save_period=0; 
row_cache_size_in_mb=0; 
rpc_address=0.0.0.0; 
rpc_interface=null; 
rpc_interface_prefer_ipv6=false; 
rpc_keepalive=true; 
rpc_listen_backlog=50; 
rpc_max_threads=2147483647; 
rpc_min_threads=16; 
rpc_port=9160; 
rpc_recv_buff_size_in_bytes=null; 
rpc_send_buff_size_in_bytes=null; 
rpc_server_type=sync; 
saved_caches_directory=/var/lib/cassandra/saved_caches; 
seed_provider=org.apache.cassandra.locator.SimpleSeedProvider{seeds=cass1}; server_encryption_options=<REDACTED>; 
snapshot_before_compaction=false; 
ssl_storage_port=7001; 
sstable_preemptive_open_interval_in_mb=50; 
start_native_transport=true; 
start_rpc=false; storage_port=7000; 
stream_throughput_outbound_megabits_per_sec=200; 
streaming_socket_timeout_in_ms=86400000; 
thrift_framed_transport_size_in_mb=15; 
thrift_max_message_length_in_mb=16; 
thrift_prepared_statements_cache_size_mb=null; 
tombstone_failure_threshold=100000; 
tombstone_warn_threshold=1000; 
tracetype_query_ttl=86400; 
tracetype_repair_ttl=604800; 
transparent_data_encryption_options=org.apache.cassandra.config.TransparentDataEncryptionOptions@27ae2fd0; 
trickle_fsync=false; 
trickle_fsync_interval_in_kb=10240; 
truncate_request_timeout_in_ms=60000; 
unlogged_batch_across_partitions_warn_threshold=10; 
user_defined_function_fail_timeout=1500; 
user_defined_function_warn_timeout=500; 
user_function_timeout_policy=die; 
windows_timer_interval=1;
write_request_timeout_in_ms=2000

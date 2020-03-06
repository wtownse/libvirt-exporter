# Prometheus libvirt exporter
Project forked from https://github.com/kumina/libvirt_exporter and substantially rewritten.
Implemented support for several additional metrics, ceph rbd (and network block devices), ovs.
Implemented statistics collection using GetAllDomainStats

And then forked again from https://github.com/rumanzo/libvirt_exporter_improved and rewritten.
Implemented meta metrics and more info about disks, interfaces and domain.

And forked again from https://github.com/AlexZzz/libvirt-exporter
Implemented title metric to work with opennebula domains.  There the name in sunstone is the title.

This repository provides code for a Prometheus metrics exporter
for [libvirt](https://libvirt.org/). This exporter connects to any
libvirt daemon and exports per-domain metrics related to CPU, memory,
disk and network usage. By default, this exporter listens on TCP port
9177.

This exporter makes use of
[libvirt-go](https://github.com/libvirt/libvirt-go), the official Go
bindings for libvirt. This exporter make use of the
`GetAllDomainStats()`

The following metrics/labels are being exported:

```
libvirt_domain_block_meta{bus="...",cache="...",discard="...",disk_type="...",domain="...",driver_type="...",serial="...",source_file="...",target_device="...",title=""}
libvirt_domain_block_stats_allocation{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_capacity{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_flush_requests_total{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_flush_total{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_physicalsize{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_read_bytes_total{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_read_requests_total{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_read_time_total{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_write_bytes_total{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_write_requests_total{domain="-...",target_device="...",title=""}
libvirt_domain_block_stats_write_time_total{domain="-...",target_device="...",title=""}

libvirt_domain_info_cpu_time_seconds_total{domain="-...",title=""}
libvirt_domain_info_maximum_memory_bytes{domain="-...",title=""}
libvirt_domain_info_memory_usage_bytes{domain="-...",title=""}
libvirt_domain_info_meta{domain="...",flavor="...",instance_name="...",project_name="...",project_uuid="...",root_type="...",root_uuid="...",user_name="...",user_uuid="...",uuid="...",title=""}
libvirt_domain_info_virtual_cpus{domain="...",title=""}
libvirt_domain_info_vstate{domain="...",title=""}

libvirt_domain_interface_meta{virtual_interface="...",domain="...",source_bridge="...",target_device="...",title=""}
libvirt_domain_interface_stats_receive_bytes_total{domain="...",target_device="...",title=""}
libvirt_domain_interface_stats_receive_drops_total{domain="...",target_device="...",title=""}
libvirt_domain_interface_stats_receive_errors_total{domain="...",target_device="...",title=""}
libvirt_domain_interface_stats_receive_packets_total{domain="...",target_device="...",title=""}
libvirt_domain_interface_stats_transmit_bytes_total{domain="...",target_device="...",title=""}
libvirt_domain_interface_stats_transmit_drops_total{domain="...",target_device="...",title=""}
libvirt_domain_interface_stats_transmit_errors_total{domain="...",target_device="...",title=""}
libvirt_domain_interface_stats_transmit_packets_total{domain="...",target_device="...",title=""}

libvirt_domain_memory_stats_actual_balloon{domain="...",title=""}
libvirt_domain_memory_stats_available{domain="...",title=""}
libvirt_domain_memory_stats_disk_cache{domain="...",title=""}
libvirt_domain_memory_stats_major_fault{domain="...",title=""}
libvirt_domain_memory_stats_minor_fault{domain="...",title=""}
libvirt_domain_memory_stats_rss{domain="...",title=""}
libvirt_domain_memory_stats_unused{domain="...",title=""}
libvirt_domain_memory_stats_usable{domain="...",title=""}
libvirt_domain_memory_stats_used_percent{domain="...",title=""}

libvirt_up
```

Repository contains a shell script, `build_static.sh`, that builds a
statically linked copy of this exporter in an Alpine Linux based
container.

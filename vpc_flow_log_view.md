## VPC Flow Log View        

The following Athena command will create the view needed for VPC Flow Log visualization.

```SQL
CREATE OR REPLACE VIEW "security_insights_vpc_vw2" AS
SELECT
metadata.product.version metadata_product_version
, metadata.product.name metadata_product_name
, metadata.product.feature.name metadata_product_feature_name
, metadata.product.vendor_name metadata_product_vendor_name
, metadata.profiles metadata_profiles
, metadata.version metadata_version
, cloud.account.uid cloud_account_uid
, cloud.region cloud_region
, cloud.zone cloud_zone
, cloud.provider cloud_provider
, src_endpoint.port src_endpoint_port
, src_endpoint.svc_name src_endpoint_svc_name
, src_endpoint.ip src_endpoint_ip
, src_endpoint.intermediate_ips src_endpoint_intermediate_ips
, src_endpoint.interface_uid src_endpoint_interface_uid
, src_endpoint.vpc_uid src_endpoint_vpc_uid
, src_endpoint.instance_uid src_endpoint_instance_uid
, src_endpoint.subnet_uid src_endpoint_subnet_uid
, dst_endpoint.port dst_endpoint_port
, dst_endpoint.svc_name dst_endpoint_svc_name
, dst_endpoint.ip dst_endpoint_ip
, dst_endpoint.intermediate_ips dst_endpoint_intermediate_ips
, dst_endpoint.interface_uid dst_endpoint_interface_uid
, dst_endpoint.vpc_uid dst_endpoint_vpc_uid
, dst_endpoint.instance_uid dst_endpoint_instance_uid
, dst_endpoint.subnet_uid dst_endpoint_subnet_uid
, connection_info.protocol_num connection_info_protocol_num
, connection_info.tcp_flags connection_info_tcp_flags
, connection_info.protocol_ver connection_info_protocol_ver
, connection_info.boundary_id connection_info_boundary_id
, connection_info.boundary connection_info_boundary
, connection_info.direction_id connection_info_direction_id
, connection_info.direction connection_info_direction
, traffic.packets traffic_packets
, traffic.bytes traffic_bytes
, time time
, time_dt time_dt
, start_time_dt start_time_dt
, end_time_dt end_time_dt
, status_code status_code
, severity_id severity_id
, severity severity
, class_name class_name
, class_uid class_uid
, category_name category_name
, category_uid category_uid
, activity_name activity_name
, activity_id activity_id
, action action
, action_id action_id
, disposition disposition
, type_uid type_uid
, type_name type_name
, accountid accountid
, region region
, asl_version asl_version
, unmapped unmapped
, observables observables
FROM
security_lake_visualization.securitylake_shared_resourcelink_vpcflow_2_0_us_east_1
WHERE (time_dt BETWEEN (current_timestamp - INTERVAL '8' DAY) AND (current_timestamp - INTERVAL '1' DAY))
```
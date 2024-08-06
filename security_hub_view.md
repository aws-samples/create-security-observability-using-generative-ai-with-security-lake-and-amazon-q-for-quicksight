## Security Hub View        

The following Athena command will create the view needed for Security Hub visualization.

```SQL
CREATE OR REPLACE VIEW "security_insights_security_hub_vw2" AS
SELECT
metadata.log_version metadata_log_version
, metadata.product.version metadata_product_version
, metadata.product.uid metadata_product_uid
, metadata.product.name metadata_product_name
, metadata.product.vendor_name metadata_product_vendor_name
, metadata.product.feature.uid metadata_product_feature_uid
, metadata.product.feature.name metadata_product_feature_name
, metadata.processed_time_dt metadata_processed_time_dt
, metadata.profiles metadata_profiles
, metadata.version metadata_version
, metadata.extensions metadata_extensions
, time time
, time_dt time_dt
, confidence_score confidence_score
, message message
, cloud.account.uid cloud_account_uid
, cloud.region cloud_region
, cloud.provider cloud_provider
, resource.type resource_type
, resource.uid resource_uid
, resource.cloud_partition resource_cloud_partition
, resource.region resource_region
, resource.labels resource_labels
, resource.data resource_data
, resource.criticality resource_criticality
, finding_info.created_time_dt finding_info_created_time_dt
, finding_info.uid finding_info_uid
, finding_info.desc finding_info_desc
, finding_info.title finding_info_title
, finding_info.modified_time_dt finding_info_modified_time_dt
, finding_info.first_seen_time_dt finding_info_first_seen_time_dt
, finding_info.last_seen_time_dt finding_info_last_seen_time_dt
, finding_info.related_events finding_info_related_events
, finding_info.types finding_info_types
, finding_info.src_url finding_info_src_url
, remediation.desc remediation_desc
, remediation.references remediation_references
, compliance.standards compliance_standards
, compliance.requirements compliance_requirements
, compliance.control compliance_control
, compliance.status compliance_status
, compliance.status_detail compliance_status_detail
, compliance.status_code compliance_status_code
, vulnerabilities vulnerabilities
, resources resources
, evidences evidences
, class_name class_name
, class_uid class_uid
, category_name category_name
, category_uid category_uid
, severity_id severity_id
, severity severity
, activity_name activity_name
, activity_id activity_id
, type_uid type_uid
, type_name type_name
, status status
, unmapped unmapped
, accountid accountid
, region region
, asl_version asl_version
, observables observables
, observables[1].value as "Instance Id"
, unmapped['ProductFields.aws/inspector/inspectorScore'] as "Inspector Score"
, vulnerabilities[1].cve.epss.score as "EPSS Score"
, unmapped['ProductFields.aws/inspector/resources/1/resourceDetails/awsEc2InstanceDetails/platform'] as "Operating System"
, vulnerabilities[1].is_fix_available as "Vulnfix Available"
, vulnerabilities[1].is_exploit_available as "Exploit Available"
FROM
security_lake_visualization.securitylake_shared_resourcelink_securityhub_2_0_us_east_1
WHERE (time_dt BETWEEN (current_timestamp - INTERVAL '8' DAY) AND (current_timestamp - INTERVAL '1' DAY))
```
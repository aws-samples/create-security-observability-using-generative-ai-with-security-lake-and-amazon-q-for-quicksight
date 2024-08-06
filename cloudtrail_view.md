## CloudTrail View        

The following Athena command will create the view needed for CloudTrail visualization.

```SQL
CREATE OR REPLACE VIEW "security_insights_cloudtrail_vw2" AS
SELECT
metadata.product.version metadata_product_version
, metadata.product.name metadata_product_name
, metadata.product.vendor_name metadata_product_vendor_name
, metadata.product.feature.name metadata_product_feature_name
, metadata.event_code metadata_event_code
, metadata.uid metadata_uid
, metadata.profiles metadata_profiles
, metadata.version metadata_version
, time time
, time_dt time_dt
, cloud.region cloud_region
, cloud.provider cloud_provider
, api.response.error api_response_error
, api.response.message api_response_message
, api.response.data api_response_data
, api.operation api_operation
, api.version api_version
, api.service.name api_service_name
, api.request.data api_request_data
, api.request.uid api_request_uid
, dst_endpoint.svc_name dst_endpoint_svc_name
, actor.user.type actor_user_type
, actor.user.name actor_user_name
, actor.user.uid_alt actor_user_uid_alt
, actor.user.uid actor_user_uid
, actor.user.account.uid actor_user_account_uid
, actor.user.credential_uid actor_user_credential_uid
, actor.session.created_time_dt actor_session_created_time_dt
, actor.session.is_mfa actor_session_is_mfa
, actor.session.issuer actor_session_issuer
, actor.invoked_by actor_invoked_by
, actor.idp.name actor_idp_name
, http_request.user_agent http_request_user_agent
, src_endpoint.uid src_endpoint_uid
, src_endpoint.ip src_endpoint_ip
, src_endpoint.domain src_endpoint_domain
, session.uid session_uid
, session.uid_alt session_uid_alt
, session.credential_uid session_credential_uid
, session.issuer session_issuer
, policy.uid policy_uid
, resources resources
, class_name class_name
, class_uid class_uid
, category_name category_name
, category_uid category_uid
, severity_id severity_id
, severity severity
, user.uid_alt user_uid_alt
, user.uid user_uid
, user.name user_name
, activity_name activity_name
, activity_id activity_id
, type_uid type_uid
, type_name type_name
, status status
, is_mfa is_mfa
, unmapped unmapped
, accountid accountid
, region region
, asl_version asl_version
, observables observables
FROM
security_lake_visualization.securitylake_shared_resourcelink_cloudtrail_2_0_us_east_1
WHERE (time_dt BETWEEN (current_timestamp - INTERVAL '8' DAY) AND (current_timestamp - INTERVAL '1' DAY))
```
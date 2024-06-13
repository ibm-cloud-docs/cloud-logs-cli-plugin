---

copyright:
  years:  2024
lastupdated: "2024-05-14"

keywords:

subcollection: cloud-logs

---

# {{site.data.keyword.logs_full_notm}} CLI
{: #cloud-logs-cli}

You can use the {{site.data.keyword.logs_full}} command-line interface (CLI) to manage your {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Prerequisites
{: #logs-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.logs_full_notm}} CLI plug-in by running the following command:

    ```text
    ibmcloud plugin install logs
    ```
    {: pre}

    You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
    {: tip}

* To target the {{site.data.keyword.logs_full_notm}} instance, use one of the following options.

    * Run the `ibmcloud logs config set` command.

      ```text
       ibmcloud logs config set service-url https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}


    * Export an environment variable with your {{site.data.keyword.logs_full_notm}} service endpoint URL.

      ```text
      export LOGS_URL=https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}

    * Set the service endpoint in the command.

      ```text
      ibmcloud logs --service-url https://{instance_ID}.api.{region}.logs.cloud.ibm.com
      ```
      {: pre}

    Replace `{instance_ID}` and `{region}` with the values that apply to your {{site.data.keyword.logs_full_notm}} service instance. The endpoint URL that is specific to your instance can be copied from the service details page in the {{site.data.keyword.logs_full_notm}} UI.

## Global configuration commands
{: #cloud-logs-globals}

Global parameters can also be stored in persistent configuration so that they do not need to be manually specified each time the plugin is invoked. Each parameter can be configured with the `config` command and its subcommands.

### `ibmcloud cloud-logs config`
{: #cloud-logs-cli-config-command}

```text
ibmcloud cloud-logs config
```
{: pre}

### `ibmcloud cloud-logs config set`
{: #cloud-logs-cli-config-set-command}

Set a new config value for a specific option. The `value` must be of type string.

```text
ibmcloud cloud-logs config set <option> <value>
```

#### Examples
{: #cloud-logs-config-set-command-examples}

```text
ibmcloud cloud-logs config set service-url \
    'https://ibm.cloud.com/my-api'
```
{: pre}

### `ibmcloud cloud-logs config get`
{: #cloud-logs-cli-config-get-command}

Display the currently set value for a specific option.

```text
ibmcloud cloud-logs config get <option>
```
{: pre}

#### Examples
{: #cloud-logs-config-get-command-examples}

```text
ibmcloud cloud-logs config get service-url
```
{: pre}

### `ibmcloud cloud-logs config unset`
{: #cloud-logs-cli-config-unset-command}

Unset the currently set value for a specific option.

The options available for this service are: `service-url`, .

```text
ibmcloud cloud-logs config unset <option>
```

#### Examples
{: #cloud-logs-config-unset-command-examples}

```text
ibmcloud cloud-logs config unset service-url
```
{: pre}

### `ibmcloud cloud-logs config list`
{: #cloud-logs-cli-config-list-command}

List out all of the currently set config values.

```text
ibmcloud cloud-logs config list
```
{: pre}

#### Examples
{: #cloud-logs-config-list-command-examples}

```text
ibmcloud cloud-logs config list
```
{: pre}

## AlertService
{: #cloud-logs-alert-service-cli}

Create and manage alerts.

### `ibmcloud cloud-logs alert`
{: #cloud-logs-cli-alert-command}

Get an alert by ID.

```text
ibmcloud cloud-logs alert --id ID
```


#### Command options
{: #cloud-logs-alert-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-alert-examples}

```text
ibmcloud cloud-logs alert \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs alert-update`
{: #cloud-logs-cli-alert-update-command}

Update an alert.

```text
ibmcloud cloud-logs alert-update --id ID --name NAME --is-active IS-ACTIVE --severity SEVERITY [--condition CONDITION | --condition-immediate CONDITION-IMMEDIATE --condition-less-than CONDITION-LESS-THAN --condition-more-than CONDITION-MORE-THAN --condition-more-than-usual CONDITION-MORE-THAN-USUAL --condition-new-value CONDITION-NEW-VALUE --condition-flow CONDITION-FLOW --condition-unique-count CONDITION-UNIQUE-COUNT --condition-less-than-usual CONDITION-LESS-THAN-USUAL] --notification-groups NOTIFICATION-GROUPS [--filters FILTERS | --filters-severities FILTERS-SEVERITIES --filters-metadata FILTERS-METADATA --filters-alias FILTERS-ALIAS --filters-text FILTERS-TEXT --filters-ratio-alerts FILTERS-RATIO-ALERTS --filters-filter-type FILTERS-FILTER-TYPE] [--description DESCRIPTION] [--expiration EXPIRATION | --expiration-year EXPIRATION-YEAR --expiration-month EXPIRATION-MONTH --expiration-day EXPIRATION-DAY] [--active-when ACTIVE-WHEN | --active-when-timeframes ACTIVE-WHEN-TIMEFRAMES] [--notification-payload-filters NOTIFICATION-PAYLOAD-FILTERS] [--meta-labels META-LABELS] [--meta-labels-strings META-LABELS-STRINGS] [--incident-settings INCIDENT-SETTINGS | --incident-settings-retriggering-period-seconds INCIDENT-SETTINGS-RETRIGGERING-PERIOD-SECONDS --incident-settings-notify-on INCIDENT-SETTINGS-NOTIFY-ON --incident-settings-use-as-notification-settings INCIDENT-SETTINGS-USE-AS-NOTIFICATION-SETTINGS]
```


#### Command options
{: #cloud-logs-alert-update-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   Alert name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--is-active` (bool)
:   Alert is active. Required.

`--severity` (string)
:   Alert severity. Required.

    Allowable values are: `info_or_unspecified`, `warning`, `critical`, `error`.

`--condition` ([`AlertsV2AlertCondition`](#cli-alerts-v2-alert-condition-example-schema))
:   Alert condition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition=@path/to/file.json`.

`--notification-groups` ([`AlertsV2AlertNotificationGroups[]`](#cli-alerts-v2-alert-notification-groups-example-schema))
:   Alert notification groups. Required.

    The maximum length is `10` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-groups=@path/to/file.json`.

`--filters` ([`AlertsV1AlertFilters`](#cli-alerts-v1-alert-filters-example-schema))
:   Alert filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--description` (string)
:   Alert description.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--expiration` ([`AlertsV1Date`](#cli-alerts-v1-date-example-schema))
:   Alert expiration date. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--expiration=@path/to/file.json`.

`--active-when` ([`AlertsV1AlertActiveWhen`](#cli-alerts-v1-alert-active-when-example-schema))
:   When should the alert be active. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when=@path/to/file.json`.

`--notification-payload-filters` ([]string)
:   JSON keys to include in the alert notification, if left empty get the full log text in the alert notification.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `100` items. The minimum length is `0` items.

`--meta-labels` ([`AlertsV1MetaLabel[]`](#cli-alerts-v1-meta-label-example-schema))
:   The Meta labels to add to the alert.

    The maximum length is `200` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--meta-labels=@path/to/file.json`.

`--meta-labels-strings` ([]string)
:   The Meta labels to add to the alert as string with ':' separator.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

`--incident-settings` ([`AlertsV2AlertIncidentSettings`](#cli-alerts-v2-alert-incident-settings-example-schema))
:   Incident settings, will create the incident based on this configuration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--incident-settings=@path/to/file.json`.

`--condition-immediate` ([`AlertsV2ImmediateConditionEmpty`](#cli-alerts-v2-immediate-condition-empty-example-schema))
:   Condition for immediate standard alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-immediate=@path/to/file.json`.

`--condition-less-than` ([`AlertsV2LessThanCondition`](#cli-alerts-v2-less-than-condition-example-schema))
:   Condition for less than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than=@path/to/file.json`.

`--condition-more-than` ([`AlertsV2MoreThanCondition`](#cli-alerts-v2-more-than-condition-example-schema))
:   Condition for more than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than=@path/to/file.json`.

`--condition-more-than-usual` ([`AlertsV2MoreThanUsualCondition`](#cli-alerts-v2-more-than-usual-condition-example-schema))
:   Condition for more than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than-usual=@path/to/file.json`.

`--condition-new-value` ([`AlertsV2NewValueCondition`](#cli-alerts-v2-new-value-condition-example-schema))
:   Condition for new value alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-new-value=@path/to/file.json`.

`--condition-flow` ([`AlertsV2FlowCondition`](#cli-alerts-v2-flow-condition-example-schema))
:   Condition for flow alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-flow=@path/to/file.json`.

`--condition-unique-count` ([`AlertsV2UniqueCountCondition`](#cli-alerts-v2-unique-count-condition-example-schema))
:   Condition for unique count alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-unique-count=@path/to/file.json`.

`--condition-less-than-usual` ([`AlertsV2LessThanUsualCondition`](#cli-alerts-v2-less-than-usual-condition-example-schema))
:   Condition for less than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than-usual=@path/to/file.json`.

`--filters-severities` ([]string)
:   The severity of the logs to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable list items are: `debug_or_unspecified`, `verbose`, `info`, `warning`, `error`, `critical`. The maximum length is `4096` items. The minimum length is `0` items.

`--filters-metadata` ([`AlertsV1AlertFiltersMetadataFilters`](#cli-alerts-v1-alert-filters-metadata-filters-example-schema))
:   The metadata filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-metadata=@path/to/file.json`.

`--filters-alias` (string)
:   The alias of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-text` (string)
:   The text to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-ratio-alerts` ([`AlertsV1AlertFiltersRatioAlert[]`](#cli-alerts-v1-alert-filters-ratio-alert-example-schema))
:   The ratio alerts. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-ratio-alerts=@path/to/file.json`.

`--filters-filter-type` (string)
:   The type of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable values are: `text_or_unspecified`, `template`, `ratio`, `unique_count`, `time_relative`, `metric`, `flow`.

`--expiration-year` (int64)
:   Year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-month` (int64)
:   Month of the year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-day` (int64)
:   Day of the month. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--active-when-timeframes` ([`AlertsV1AlertActiveTimeframe[]`](#cli-alerts-v1-alert-active-timeframe-example-schema))
:   Activity timeframes of the alert. This option provides a value for a sub-field of the JSON option 'active-when'. It is mutually exclusive with that option.

    The maximum length is `30` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when-timeframes=@path/to/file.json`.

`--incident-settings-retriggering-period-seconds` (int64)
:   The retriggering period of the alert in seconds. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    The maximum value is `4294967295`. The minimum value is `0`.

`--incident-settings-notify-on` (string)
:   Notify on setting. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    Allowable values are: `triggered_only`, `triggered_and_resolved`.

`--incident-settings-use-as-notification-settings` (bool)
:   Use these settings for all notificaion webhook. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

#### Examples
{: #cloud-logs-alert-update-examples}

```text
ibmcloud cloud-logs alert-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --condition '{"more_than": {"parameters": {"threshold": 1, "timeframe": "timeframe_10_min", "group_by": ["coralogix.metadata.applicationName"], "metric_alert_parameters": {"metric_field": "cpu_usage", "metric_source": "prometheus", "arithmetic_operator": "percentile", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "metric_alert_promql_parameters": {"promql_text": "sum(rate(container_cpu_usage_seconds_total{container_name=\"my-container\"}[5m])) by (pod_name)", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "ignore_infinity": true, "relative_timeframe": "hour_or_unspecified", "cardinality_fields": [], "related_extended_data": {"cleanup_deadman_duration": "cleanup_deadman_duration_24h", "should_trigger_deadman": true}}, "evaluation_window": "rolling_or_unspecified"}}' \
    --notification-groups '[{"group_by_fields": ["coralogix.metadata.applicationName"], "notifications": [{"retriggering_period_seconds": 60, "notify_on": "triggered_and_resolved", "integration_id": 123}]}]' \
    --filters '{"severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "metadata": {"applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"]}, "alias": "monitorQuery", "text": "initiator.id.keyword:iam-ServiceId-10820fd6-c3fe-414e-8fd5-44ce95f7d34d AND action.keyword:cloud-object-storage.object.create", "ratio_alerts": [{"alias": "TopLevelAlert", "text": "_exists_:\"container_name\"", "severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"], "group_by": ["Host","Thread"]}], "filter_type": "text_or_unspecified"}' \
    --description 'Alert if the number of logs reaches a threshold' \
    --expiration '{"year": 2012, "month": 12, "day": 24}' \
    --active-when '{"timeframes": [{"days_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "range": {"start": {"hours": 18, "minutes": 30, "seconds": 0}, "end": {"hours": 18, "minutes": 30, "seconds": 0}}}]}' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[{"key": "env", "value": "dev"}]' \
    --meta-labels-strings '[]' \
    --incident-settings '{"retriggering_period_seconds": 300, "notify_on": "triggered_only", "use_as_notification_settings": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs alert-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --notification-groups '[alertsV2AlertNotificationGroups]' \
    --description 'Alert if the number of logs reaches a threshold' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[alertsV1MetaLabel]' \
    --meta-labels-strings '[]' \
    --condition-immediate alertsV2ImmediateConditionEmpty \
    --condition-less-than alertsV2LessThanCondition \
    --condition-more-than alertsV2MoreThanCondition \
    --condition-more-than-usual alertsV2MoreThanUsualCondition \
    --condition-new-value alertsV2NewValueCondition \
    --condition-flow alertsV2FlowCondition \
    --condition-unique-count alertsV2UniqueCountCondition \
    --condition-less-than-usual alertsV2LessThanUsualCondition \
    --filters-severities debug_or_unspecified,verbose,info,warning,error,critical \
    --filters-metadata alertsV1AlertFiltersMetadataFilters \
    --filters-alias monitorQuery \
    --filters-text _exists_:"container_name" \
    --filters-ratio-alerts '[alertsV1AlertFiltersRatioAlert]' \
    --filters-filter-type flow \
    --expiration-year 2012 \
    --expiration-month 12 \
    --expiration-day 24 \
    --active-when-timeframes '[alertsV1AlertActiveTimeframe]' \
    --incident-settings-retriggering-period-seconds 60 \
    --incident-settings-notify-on triggered_and_resolved \
    --incident-settings-use-as-notification-settings true
```
{: pre}

### `ibmcloud cloud-logs alert-delete`
{: #cloud-logs-cli-alert-delete-command}

Delete an alert.

```text
ibmcloud cloud-logs alert-delete --id ID
```


#### Command options
{: #cloud-logs-alert-delete-cli-options}

`--id` (strfmt.UUID)
:   Alert ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-alert-delete-examples}

```text
ibmcloud cloud-logs alert-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs alerts`
{: #cloud-logs-cli-alerts-command}

List alerts.

```text
ibmcloud cloud-logs alerts
```


#### Example
{: #cloud-logs-alerts-examples}

```text
ibmcloud cloud-logs alerts
```
{: pre}

### `ibmcloud cloud-logs alert-create`
{: #cloud-logs-cli-alert-create-command}

Create an alert.

```text
ibmcloud cloud-logs alert-create --name NAME --is-active IS-ACTIVE --severity SEVERITY [--condition CONDITION | --condition-immediate CONDITION-IMMEDIATE --condition-less-than CONDITION-LESS-THAN --condition-more-than CONDITION-MORE-THAN --condition-more-than-usual CONDITION-MORE-THAN-USUAL --condition-new-value CONDITION-NEW-VALUE --condition-flow CONDITION-FLOW --condition-unique-count CONDITION-UNIQUE-COUNT --condition-less-than-usual CONDITION-LESS-THAN-USUAL] --notification-groups NOTIFICATION-GROUPS [--filters FILTERS | --filters-severities FILTERS-SEVERITIES --filters-metadata FILTERS-METADATA --filters-alias FILTERS-ALIAS --filters-text FILTERS-TEXT --filters-ratio-alerts FILTERS-RATIO-ALERTS --filters-filter-type FILTERS-FILTER-TYPE] [--description DESCRIPTION] [--expiration EXPIRATION | --expiration-year EXPIRATION-YEAR --expiration-month EXPIRATION-MONTH --expiration-day EXPIRATION-DAY] [--active-when ACTIVE-WHEN | --active-when-timeframes ACTIVE-WHEN-TIMEFRAMES] [--notification-payload-filters NOTIFICATION-PAYLOAD-FILTERS] [--meta-labels META-LABELS] [--meta-labels-strings META-LABELS-STRINGS] [--incident-settings INCIDENT-SETTINGS | --incident-settings-retriggering-period-seconds INCIDENT-SETTINGS-RETRIGGERING-PERIOD-SECONDS --incident-settings-notify-on INCIDENT-SETTINGS-NOTIFY-ON --incident-settings-use-as-notification-settings INCIDENT-SETTINGS-USE-AS-NOTIFICATION-SETTINGS]
```


#### Command options
{: #cloud-logs-alert-create-cli-options}

`--name` (string)
:   Alert name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--is-active` (bool)
:   Alert is active. Required.

`--severity` (string)
:   Alert severity. Required.

    Allowable values are: `info_or_unspecified`, `warning`, `critical`, `error`.

`--condition` ([`AlertsV2AlertCondition`](#cli-alerts-v2-alert-condition-example-schema))
:   Alert condition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition=@path/to/file.json`.

`--notification-groups` ([`AlertsV2AlertNotificationGroups[]`](#cli-alerts-v2-alert-notification-groups-example-schema))
:   Alert notification groups. Required.

    The maximum length is `10` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--notification-groups=@path/to/file.json`.

`--filters` ([`AlertsV1AlertFilters`](#cli-alerts-v1-alert-filters-example-schema))
:   Alert filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--description` (string)
:   Alert description.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--expiration` ([`AlertsV1Date`](#cli-alerts-v1-date-example-schema))
:   Alert expiration date. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--expiration=@path/to/file.json`.

`--active-when` ([`AlertsV1AlertActiveWhen`](#cli-alerts-v1-alert-active-when-example-schema))
:   When should the alert be active. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when=@path/to/file.json`.

`--notification-payload-filters` ([]string)
:   JSON keys to include in the alert notification, if left empty get the full log text in the alert notification.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `100` items. The minimum length is `0` items.

`--meta-labels` ([`AlertsV1MetaLabel[]`](#cli-alerts-v1-meta-label-example-schema))
:   The Meta labels to add to the alert.

    The maximum length is `200` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--meta-labels=@path/to/file.json`.

`--meta-labels-strings` ([]string)
:   The Meta labels to add to the alert as string with ':' separator.

    The list items must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`. The maximum length is `4096` items. The minimum length is `0` items.

`--incident-settings` ([`AlertsV2AlertIncidentSettings`](#cli-alerts-v2-alert-incident-settings-example-schema))
:   Incident settings, will create the incident based on this configuration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--incident-settings=@path/to/file.json`.

`--condition-immediate` ([`AlertsV2ImmediateConditionEmpty`](#cli-alerts-v2-immediate-condition-empty-example-schema))
:   Condition for immediate standard alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-immediate=@path/to/file.json`.

`--condition-less-than` ([`AlertsV2LessThanCondition`](#cli-alerts-v2-less-than-condition-example-schema))
:   Condition for less than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than=@path/to/file.json`.

`--condition-more-than` ([`AlertsV2MoreThanCondition`](#cli-alerts-v2-more-than-condition-example-schema))
:   Condition for more than alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than=@path/to/file.json`.

`--condition-more-than-usual` ([`AlertsV2MoreThanUsualCondition`](#cli-alerts-v2-more-than-usual-condition-example-schema))
:   Condition for more than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-more-than-usual=@path/to/file.json`.

`--condition-new-value` ([`AlertsV2NewValueCondition`](#cli-alerts-v2-new-value-condition-example-schema))
:   Condition for new value alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-new-value=@path/to/file.json`.

`--condition-flow` ([`AlertsV2FlowCondition`](#cli-alerts-v2-flow-condition-example-schema))
:   Condition for flow alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-flow=@path/to/file.json`.

`--condition-unique-count` ([`AlertsV2UniqueCountCondition`](#cli-alerts-v2-unique-count-condition-example-schema))
:   Condition for unique count alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-unique-count=@path/to/file.json`.

`--condition-less-than-usual` ([`AlertsV2LessThanUsualCondition`](#cli-alerts-v2-less-than-usual-condition-example-schema))
:   Condition for less than usual alert. This option provides a value for a sub-field of the JSON option 'condition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--condition-less-than-usual=@path/to/file.json`.

`--filters-severities` ([]string)
:   The severity of the logs to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable list items are: `debug_or_unspecified`, `verbose`, `info`, `warning`, `error`, `critical`. The maximum length is `4096` items. The minimum length is `0` items.

`--filters-metadata` ([`AlertsV1AlertFiltersMetadataFilters`](#cli-alerts-v1-alert-filters-metadata-filters-example-schema))
:   The metadata filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-metadata=@path/to/file.json`.

`--filters-alias` (string)
:   The alias of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-text` (string)
:   The text to filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--filters-ratio-alerts` ([`AlertsV1AlertFiltersRatioAlert[]`](#cli-alerts-v1-alert-filters-ratio-alert-example-schema))
:   The ratio alerts. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-ratio-alerts=@path/to/file.json`.

`--filters-filter-type` (string)
:   The type of the filter. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    Allowable values are: `text_or_unspecified`, `template`, `ratio`, `unique_count`, `time_relative`, `metric`, `flow`.

`--expiration-year` (int64)
:   Year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-month` (int64)
:   Month of the year. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--expiration-day` (int64)
:   Day of the month. This option provides a value for a sub-field of the JSON option 'expiration'. It is mutually exclusive with that option.

`--active-when-timeframes` ([`AlertsV1AlertActiveTimeframe[]`](#cli-alerts-v1-alert-active-timeframe-example-schema))
:   Activity timeframes of the alert. This option provides a value for a sub-field of the JSON option 'active-when'. It is mutually exclusive with that option.

    The maximum length is `30` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--active-when-timeframes=@path/to/file.json`.

`--incident-settings-retriggering-period-seconds` (int64)
:   The retriggering period of the alert in seconds. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    The maximum value is `4294967295`. The minimum value is `0`.

`--incident-settings-notify-on` (string)
:   Notify on setting. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

    Allowable values are: `triggered_only`, `triggered_and_resolved`.

`--incident-settings-use-as-notification-settings` (bool)
:   Use these settings for all notificaion webhook. This option provides a value for a sub-field of the JSON option 'incident-settings'. It is mutually exclusive with that option.

#### Examples
{: #cloud-logs-alert-create-examples}

```text
ibmcloud cloud-logs alert-create \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --condition '{"more_than": {"parameters": {"threshold": 1, "timeframe": "timeframe_10_min", "group_by": ["coralogix.metadata.applicationName"], "metric_alert_parameters": {"metric_field": "cpu_usage", "metric_source": "prometheus", "arithmetic_operator": "percentile", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "metric_alert_promql_parameters": {"promql_text": "sum(rate(container_cpu_usage_seconds_total{container_name=\"my-container\"}[5m])) by (pod_name)", "arithmetic_operator_modifier": 1, "sample_threshold_percentage": 100, "non_null_percentage": 100, "swap_null_values": true}, "ignore_infinity": true, "relative_timeframe": "hour_or_unspecified", "cardinality_fields": [], "related_extended_data": {"cleanup_deadman_duration": "cleanup_deadman_duration_24h", "should_trigger_deadman": true}}, "evaluation_window": "rolling_or_unspecified"}}' \
    --notification-groups '[{"group_by_fields": ["coralogix.metadata.applicationName"], "notifications": [{"retriggering_period_seconds": 60, "notify_on": "triggered_and_resolved", "integration_id": 123}]}]' \
    --filters '{"severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "metadata": {"applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"]}, "alias": "monitorQuery", "text": "initiator.id.keyword:iam-ServiceId-10820fd6-c3fe-414e-8fd5-44ce95f7d34d AND action.keyword:cloud-object-storage.object.create", "ratio_alerts": [{"alias": "TopLevelAlert", "text": "_exists_:\"container_name\"", "severities": ["debug_or_unspecified","verbose","info","warning","error","critical"], "applications": ["CpuMonitoring","WebApi"], "subsystems": ["SnapshotGenerator","PermissionControl"], "group_by": ["Host","Thread"]}], "filter_type": "text_or_unspecified"}' \
    --description 'Alert if the number of logs reaches a threshold' \
    --expiration '{"year": 2012, "month": 12, "day": 24}' \
    --active-when '{"timeframes": [{"days_of_week": ["monday_or_unspecified","tuesday","wednesday","thursday","friday","saturday","sunday"], "range": {"start": {"hours": 18, "minutes": 30, "seconds": 0}, "end": {"hours": 18, "minutes": 30, "seconds": 0}}}]}' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[{"key": "env", "value": "dev"}]' \
    --meta-labels-strings '[]' \
    --incident-settings '{"retriggering_period_seconds": 300, "notify_on": "triggered_only", "use_as_notification_settings": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs alert-create \
    --name 'Test alert' \
    --is-active true \
    --severity info_or_unspecified \
    --notification-groups '[alertsV2AlertNotificationGroups]' \
    --description 'Alert if the number of logs reaches a threshold' \
    --notification-payload-filters exampleString,anotherTestString \
    --meta-labels '[alertsV1MetaLabel]' \
    --meta-labels-strings '[]' \
    --condition-immediate alertsV2ImmediateConditionEmpty \
    --condition-less-than alertsV2LessThanCondition \
    --condition-more-than alertsV2MoreThanCondition \
    --condition-more-than-usual alertsV2MoreThanUsualCondition \
    --condition-new-value alertsV2NewValueCondition \
    --condition-flow alertsV2FlowCondition \
    --condition-unique-count alertsV2UniqueCountCondition \
    --condition-less-than-usual alertsV2LessThanUsualCondition \
    --filters-severities debug_or_unspecified,verbose,info,warning,error,critical \
    --filters-metadata alertsV1AlertFiltersMetadataFilters \
    --filters-alias monitorQuery \
    --filters-text _exists_:"container_name" \
    --filters-ratio-alerts '[alertsV1AlertFiltersRatioAlert]' \
    --filters-filter-type flow \
    --expiration-year 2012 \
    --expiration-month 12 \
    --expiration-day 24 \
    --active-when-timeframes '[alertsV1AlertActiveTimeframe]' \
    --incident-settings-retriggering-period-seconds 60 \
    --incident-settings-notify-on triggered_and_resolved \
    --incident-settings-use-as-notification-settings true
```
{: pre}

## RuleGroupsService
{: #cloud-logs-rule-groups-service-cli}

Create and manage parsing rules.

### `ibmcloud cloud-logs rule-group`
{: #cloud-logs-cli-rule-group-command}

Gets rule group by groupid.

```text
ibmcloud cloud-logs rule-group --group-id GROUP-ID
```


#### Command options
{: #cloud-logs-rule-group-cli-options}

`--group-id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-rule-group-examples}

```text
ibmcloud cloud-logs rule-group \
    --group-id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs rule-group-update`
{: #cloud-logs-cli-rule-group-update-command}

Updates rule group by groupid.

```text
ibmcloud cloud-logs rule-group-update --group-id GROUP-ID --name NAME --rule-subgroups RULE-SUBGROUPS [--description DESCRIPTION] [--enabled ENABLED] [--rule-matchers RULE-MATCHERS] [--order ORDER]
```


#### Command options
{: #cloud-logs-rule-group-update-cli-options}

`--group-id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   The name of the rule group. Required.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--rule-subgroups` ([`RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]`](#cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema))
:   Rule subgroups. Will try to execute the first rule subgroup, and if not matched will try to match the next one in order. Required.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-subgroups=@path/to/file.json`.

`--description` (string)
:   A description for the rule group, should express what is the rule group purpose.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--enabled` (bool)
:   Whether or not the rule is enabled.

`--rule-matchers` ([`RulesV1RuleMatcher[]`](#cli-rules-v1-rule-matcher-example-schema))
:   Optional rule matchers which if matched will make the rule go through the rule group.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-matchers=@path/to/file.json`.

`--order` (int64)
:   The order in which the rule group will be evaluated. The lower the order, the more priority the group will have. Not providing the order will by default create a group with the last order.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-rule-group-update-examples}

```text
ibmcloud cloud-logs rule-group-update \
    --group-id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name mysql-extractrule \
    --rule-subgroups '[{"rules": [{"name": "mysql-parse", "description": "mysql-parse", "source_field": "text", "parameters": {"parse_parameters": {"destination_field": "text", "rule": "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),\'?(?P<object>.*)\'?,(?P<returnCode>[0-9]+)"}}, "enabled": true, "order": 1}], "enabled": true, "order": 1}]' \
    --description 'mysql audit logs parser' \
    --enabled true \
    --rule-matchers '[{"subsystem_name": {"value": "mysql"}}]' \
    --order 39
```
{: pre}

### `ibmcloud cloud-logs rule-group-delete`
{: #cloud-logs-cli-rule-group-delete-command}

Deletes rule group by groupid.

```text
ibmcloud cloud-logs rule-group-delete --group-id GROUP-ID
```


#### Command options
{: #cloud-logs-rule-group-delete-cli-options}

`--group-id` (strfmt.UUID)
:   The group ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-rule-group-delete-examples}

```text
ibmcloud cloud-logs rule-group-delete \
    --group-id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs rule-groups`
{: #cloud-logs-cli-rule-groups-command}

Gets all rule groups.

```text
ibmcloud cloud-logs rule-groups
```


#### Example
{: #cloud-logs-rule-groups-examples}

```text
ibmcloud cloud-logs rule-groups
```
{: pre}

### `ibmcloud cloud-logs rule-group-create`
{: #cloud-logs-cli-rule-group-create-command}

Creates rule group.

```text
ibmcloud cloud-logs rule-group-create --name NAME --rule-subgroups RULE-SUBGROUPS [--description DESCRIPTION] [--enabled ENABLED] [--rule-matchers RULE-MATCHERS] [--order ORDER]
```


#### Command options
{: #cloud-logs-rule-group-create-cli-options}

`--name` (string)
:   The name of the rule group. Required.

    The maximum length is `255` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--rule-subgroups` ([`RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]`](#cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema))
:   Rule subgroups. Will try to execute the first rule subgroup, and if not matched will try to match the next one in order. Required.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-subgroups=@path/to/file.json`.

`--description` (string)
:   A description for the rule group, should express what is the rule group purpose.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--enabled` (bool)
:   Whether or not the rule is enabled.

`--rule-matchers` ([`RulesV1RuleMatcher[]`](#cli-rules-v1-rule-matcher-example-schema))
:   Optional rule matchers which if matched will make the rule go through the rule group.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rule-matchers=@path/to/file.json`.

`--order` (int64)
:   The order in which the rule group will be evaluated. The lower the order, the more priority the group will have. Not providing the order will by default create a group with the last order.

    The maximum value is `4294967295`. The minimum value is `0`.

#### Example
{: #cloud-logs-rule-group-create-examples}

```text
ibmcloud cloud-logs rule-group-create \
    --name mysql-extractrule \
    --rule-subgroups '[{"rules": [{"name": "mysql-parse", "description": "mysql-parse", "source_field": "text", "parameters": {"parse_parameters": {"destination_field": "text", "rule": "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),\'?(?P<object>.*)\'?,(?P<returnCode>[0-9]+)"}}, "enabled": true, "order": 1}], "enabled": true, "order": 1}]' \
    --description 'mysql audit logs  parser' \
    --enabled true \
    --rule-matchers '[{"subsystem_name": {"value": "mysql"}}]' \
    --order 39
```
{: pre}

## OutgoingWebhooksService
{: #cloud-logs-outgoing-webhooks-service-cli}

Create and manage your Outbound integrations so that you can receive alerts.

### `ibmcloud cloud-logs outgoing-webhooks`
{: #cloud-logs-cli-outgoing-webhooks-command}

List Outbound Integrations.

```text
ibmcloud cloud-logs outgoing-webhooks [--type TYPE]
```


#### Command options
{: #cloud-logs-outgoing-webhooks-cli-options}

`--type` (string)
:   The type of the deployed Outbound Integrations to list.

    Allowable values are: `ibm_event_notifications`.

#### Example
{: #cloud-logs-outgoing-webhooks-examples}

```text
ibmcloud cloud-logs outgoing-webhooks \
    --type ibm_event_notifications
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook-create`
{: #cloud-logs-cli-outgoing-webhook-create-command}

Create an Outbound Integration.

```text
ibmcloud cloud-logs outgoing-webhook-create [--outgoing-webhook-prototype OUTGOING-WEBHOOK-PROTOTYPE | --outgoing-webhook-type OUTGOING-WEBHOOK-TYPE --outgoing-webhook-name OUTGOING-WEBHOOK-NAME --outgoing-webhook-url OUTGOING-WEBHOOK-URL --outgoing-webhook-ibm-event-notifications OUTGOING-WEBHOOK-IBM-EVENT-NOTIFICATIONS]
```


#### Command options
{: #cloud-logs-outgoing-webhook-create-cli-options}

`--outgoing-webhook-prototype` ([`OutgoingWebhookPrototype`](#cli-outgoing-webhook-prototype-example-schema))
:   The input data of the Outbound Integration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--outgoing-webhook-prototype=@path/to/file.json`.

`--outgoing-webhook-type` (string)
:   The type of the deployed Outbound Integrations to list. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    Allowable values are: `ibm_event_notifications`.

`--outgoing-webhook-name` (string)
:   The name of the Outbound Integration. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--outgoing-webhook-url` (string)
:   The URL of the Outbound Integration. Null for IBM Event Notifications integration. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--outgoing-webhook-ibm-event-notifications` ([`OutgoingWebhooksV1IbmEventNotificationsConfig`](#cli-outgoing-webhooks-v1-ibm-event-notifications-config-example-schema))
:   The configuration of the IBM Event Notifications Outbound Integration. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--outgoing-webhook-ibm-event-notifications=@path/to/file.json`.

#### Examples
{: #cloud-logs-outgoing-webhook-create-examples}

```text
ibmcloud cloud-logs outgoing-webhook-create \
    --outgoing-webhook-prototype '{"type": "ibm_event_notifications", "name": "Event Notifications Integration", "url": "https://example.com", "ibm_event_notifications": {"event_notifications_instance_id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "region_id": "eu-es"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs outgoing-webhook-create \
    --outgoing-webhook-type ibm_event_notifications \
    --outgoing-webhook-name 'Event Notifications Integration' \
    --outgoing-webhook-url https://example.com \
    --outgoing-webhook-ibm-event-notifications outgoingWebhooksV1IbmEventNotificationsConfig
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook`
{: #cloud-logs-cli-outgoing-webhook-command}

Gets an Outbound Integration by ID.

```text
ibmcloud cloud-logs outgoing-webhook --id ID
```


#### Command options
{: #cloud-logs-outgoing-webhook-cli-options}

`--id` (strfmt.UUID)
:   The ID of the Outbound Integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-outgoing-webhook-examples}

```text
ibmcloud cloud-logs outgoing-webhook \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook-update`
{: #cloud-logs-cli-outgoing-webhook-update-command}

Update an Outbound Integration.

```text
ibmcloud cloud-logs outgoing-webhook-update --id ID [--outgoing-webhook-prototype OUTGOING-WEBHOOK-PROTOTYPE | --outgoing-webhook-type OUTGOING-WEBHOOK-TYPE --outgoing-webhook-name OUTGOING-WEBHOOK-NAME --outgoing-webhook-url OUTGOING-WEBHOOK-URL --outgoing-webhook-ibm-event-notifications OUTGOING-WEBHOOK-IBM-EVENT-NOTIFICATIONS]
```


#### Command options
{: #cloud-logs-outgoing-webhook-update-cli-options}

`--id` (strfmt.UUID)
:   The ID of the Outbound Integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--outgoing-webhook-prototype` ([`OutgoingWebhookPrototype`](#cli-outgoing-webhook-prototype-example-schema))
:   The input data of the Outbound Integration. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--outgoing-webhook-prototype=@path/to/file.json`.

`--outgoing-webhook-type` (string)
:   The type of the deployed Outbound Integrations to list. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    Allowable values are: `ibm_event_notifications`.

`--outgoing-webhook-name` (string)
:   The name of the Outbound Integration. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--outgoing-webhook-url` (string)
:   The URL of the Outbound Integration. Null for IBM Event Notifications integration. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--outgoing-webhook-ibm-event-notifications` ([`OutgoingWebhooksV1IbmEventNotificationsConfig`](#cli-outgoing-webhooks-v1-ibm-event-notifications-config-example-schema))
:   The configuration of the IBM Event Notifications Outbound Integration. This option provides a value for a sub-field of the JSON option 'outgoing-webhook-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--outgoing-webhook-ibm-event-notifications=@path/to/file.json`.

#### Examples
{: #cloud-logs-outgoing-webhook-update-examples}

```text
ibmcloud cloud-logs outgoing-webhook-update \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660 \
    --outgoing-webhook-prototype '{"type": "ibm_event_notifications", "name": "Event Notifications Integration", "url": "https://example.com", "ibm_event_notifications": {"event_notifications_instance_id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "region_id": "eu-es"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs outgoing-webhook-update \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660 \
    --outgoing-webhook-type ibm_event_notifications \
    --outgoing-webhook-name 'Event Notifications Integration' \
    --outgoing-webhook-url https://example.com \
    --outgoing-webhook-ibm-event-notifications outgoingWebhooksV1IbmEventNotificationsConfig
```
{: pre}

### `ibmcloud cloud-logs outgoing-webhook-delete`
{: #cloud-logs-cli-outgoing-webhook-delete-command}

Delete an Outbound Integration.

```text
ibmcloud cloud-logs outgoing-webhook-delete --id ID
```


#### Command options
{: #cloud-logs-outgoing-webhook-delete-cli-options}

`--id` (strfmt.UUID)
:   The ID of the Outbound Integration to delete. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-outgoing-webhook-delete-examples}

```text
ibmcloud cloud-logs outgoing-webhook-delete \
    --id 585bea36-bdd1-4bfb-9a26-51f1f8a12660
```
{: pre}

## PoliciesService
{: #cloud-logs-policies-service-cli}

Create and manage TCO policies.

### `ibmcloud cloud-logs policy`
{: #cloud-logs-cli-policy-command}

Gets policy by id.

```text
ibmcloud cloud-logs policy --id ID
```


#### Command options
{: #cloud-logs-policy-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-policy-examples}

```text
ibmcloud cloud-logs policy \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs policy-update`
{: #cloud-logs-cli-policy-update-command}

Updates an existing policy.

```text
ibmcloud cloud-logs policy-update --id ID [--policy-prototype POLICY-PROTOTYPE | --policy-name POLICY-NAME --policy-description POLICY-DESCRIPTION --policy-priority POLICY-PRIORITY --policy-application-rule POLICY-APPLICATION-RULE --policy-subsystem-rule POLICY-SUBSYSTEM-RULE --policy-archive-retention POLICY-ARCHIVE-RETENTION --policy-log-rules POLICY-LOG-RULES]
```


#### Command options
{: #cloud-logs-policy-update-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--policy-prototype` ([`PolicyPrototype`](#cli-policy-prototype-example-schema))
:   Create policy request. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-prototype=@path/to/file.json`.

`--policy-name` (string)
:   Policy name. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--policy-description` (string)
:   Policy description. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--policy-priority` (string)
:   The data pipeline sources that match the policy rules will go through. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Allowable values are: `type_unspecified`, `type_block`, `type_low`, `type_medium`, `type_high`.

`--policy-application-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-application-rule=@path/to/file.json`.

`--policy-subsystem-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-subsystem-rule=@path/to/file.json`.

`--policy-archive-retention` ([`QuotaV1ArchiveRetention`](#cli-quota-v1-archive-retention-example-schema))
:   Archive retention definition. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-archive-retention=@path/to/file.json`.

`--policy-log-rules` ([`QuotaV1LogRules`](#cli-quota-v1-log-rules-example-schema))
:   Log rules. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-log-rules=@path/to/file.json`.

#### Examples
{: #cloud-logs-policy-update-examples}

```text
ibmcloud cloud-logs policy-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --policy-prototype '{"name": "Med_policy", "description": "Medium policy", "priority": "type_high", "application_rule": {"rule_type_id": "is", "name": "policy-test"}, "subsystem_rule": {"rule_type_id": "is", "name": "policy-test"}, "archive_retention": {"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "log_rules": {"severities": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs policy-update \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --policy-name 'My Policy' \
    --policy-description 'My Policy Description' \
    --policy-priority type_high \
    --policy-application-rule quotaV1Rule \
    --policy-subsystem-rule quotaV1Rule \
    --policy-archive-retention quotaV1ArchiveRetention \
    --policy-log-rules quotaV1LogRules
```
{: pre}

### `ibmcloud cloud-logs policy-delete`
{: #cloud-logs-cli-policy-delete-command}

Deletes an existing policy.

```text
ibmcloud cloud-logs policy-delete --id ID
```


#### Command options
{: #cloud-logs-policy-delete-cli-options}

`--id` (strfmt.UUID)
:   ID of policy. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-policy-delete-examples}

```text
ibmcloud cloud-logs policy-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs company-policies`
{: #cloud-logs-cli-company-policies-command}

Gets policies.

```text
ibmcloud cloud-logs company-policies [--enabled-only ENABLED-ONLY] [--source-type SOURCE-TYPE]
```


#### Command options
{: #cloud-logs-company-policies-cli-options}

`--enabled-only` (bool)
:   Optionally filter only enabled policies.

`--source-type` (string)
:   Source type to filter policies by.

    Allowable values are: `unspecified`, `logs`.

#### Example
{: #cloud-logs-company-policies-examples}

```text
ibmcloud cloud-logs company-policies \
    --enabled-only true \
    --source-type logs
```
{: pre}

### `ibmcloud cloud-logs policy-create`
{: #cloud-logs-cli-policy-create-command}

Creates a new policy.

```text
ibmcloud cloud-logs policy-create [--policy-prototype POLICY-PROTOTYPE | --policy-name POLICY-NAME --policy-description POLICY-DESCRIPTION --policy-priority POLICY-PRIORITY --policy-application-rule POLICY-APPLICATION-RULE --policy-subsystem-rule POLICY-SUBSYSTEM-RULE --policy-archive-retention POLICY-ARCHIVE-RETENTION --policy-log-rules POLICY-LOG-RULES]
```


#### Command options
{: #cloud-logs-policy-create-cli-options}

`--policy-prototype` ([`PolicyPrototype`](#cli-policy-prototype-example-schema))
:   Create policy request. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-prototype=@path/to/file.json`.

`--policy-name` (string)
:   Policy name. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--policy-description` (string)
:   Policy description. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--policy-priority` (string)
:   The data pipeline sources that match the policy rules will go through. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Allowable values are: `type_unspecified`, `type_block`, `type_low`, `type_medium`, `type_high`.

`--policy-application-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-application-rule=@path/to/file.json`.

`--policy-subsystem-rule` ([`QuotaV1Rule`](#cli-quota-v1-rule-example-schema))
:   Rule for matching with application. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-subsystem-rule=@path/to/file.json`.

`--policy-archive-retention` ([`QuotaV1ArchiveRetention`](#cli-quota-v1-archive-retention-example-schema))
:   Archive retention definition. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-archive-retention=@path/to/file.json`.

`--policy-log-rules` ([`QuotaV1LogRules`](#cli-quota-v1-log-rules-example-schema))
:   Log rules. This option provides a value for a sub-field of the JSON option 'policy-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--policy-log-rules=@path/to/file.json`.

#### Examples
{: #cloud-logs-policy-create-examples}

```text
ibmcloud cloud-logs policy-create \
    --policy-prototype '{"name": "Med_policy", "description": "Medium Policy", "priority": "type_high", "application_rule": {"rule_type_id": "is", "name": "policy-test"}, "subsystem_rule": {"rule_type_id": "is", "name": "policy-test"}, "archive_retention": {"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "log_rules": {"severities": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs policy-create \
    --policy-name 'My Policy' \
    --policy-description 'My Policy Description' \
    --policy-priority type_high \
    --policy-application-rule quotaV1Rule \
    --policy-subsystem-rule quotaV1Rule \
    --policy-archive-retention quotaV1ArchiveRetention \
    --policy-log-rules quotaV1LogRules
```
{: pre}

## DashboardsService
{: #cloud-logs-dashboards-service-cli}

API to manage your dashboards.

### `ibmcloud cloud-logs dashboard-create`
{: #cloud-logs-cli-dashboard-create-command}

Creates a new dashboard.

```text
ibmcloud cloud-logs dashboard-create [--dashboard DASHBOARD | --dashboard-href DASHBOARD-HREF --dashboard-id DASHBOARD-ID --dashboard-name DASHBOARD-NAME --dashboard-description DASHBOARD-DESCRIPTION --dashboard-layout DASHBOARD-LAYOUT --dashboard-variables DASHBOARD-VARIABLES --dashboard-filters DASHBOARD-FILTERS --dashboard-annotations DASHBOARD-ANNOTATIONS --dashboard-absolute-time-frame DASHBOARD-ABSOLUTE-TIME-FRAME --dashboard-relative-time-frame DASHBOARD-RELATIVE-TIME-FRAME --dashboard-folder-id DASHBOARD-FOLDER-ID --dashboard-folder-path DASHBOARD-FOLDER-PATH --dashboard-false DASHBOARD-FALSE --dashboard-two-minutes DASHBOARD-TWO-MINUTES --dashboard-five-minutes DASHBOARD-FIVE-MINUTES]
```


#### Command options
{: #cloud-logs-dashboard-create-cli-options}

`--dashboard` ([`Dashboard`](#cli-dashboard-example-schema))
:   Dashboard represents the structure and configuration of a Coralogix Custom Dashboard. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard=@path/to/file.json`.

`--dashboard-href` (string)
:   Unique identifier for the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `21` characters. The minimum length is `21` characters. The value must match regular expression `/^[a-zA-Z0-9]{21}$/`.

`--dashboard-id` (string)
:   Unique identifier for the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `21` characters. The minimum length is `21` characters. The value must match regular expression `/^[a-zA-Z0-9]{21}$/`.

`--dashboard-name` (string)
:   Display name of the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--dashboard-description` (string)
:   Brief description or summary of the dashboard's purpose or content. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `200` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--dashboard-layout` ([`ApisDashboardsV1AstLayout`](#cli-apis-dashboards-v1-ast-layout-example-schema))
:   Layout configuration for the dashboard's visual elements. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-layout=@path/to/file.json`.

`--dashboard-variables` ([`ApisDashboardsV1AstVariable[]`](#cli-apis-dashboards-v1-ast-variable-example-schema))
:   List of variables that can be used within the dashboard for dynamic content. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-variables=@path/to/file.json`.

`--dashboard-filters` ([`ApisDashboardsV1AstFilter[]`](#cli-apis-dashboards-v1-ast-filter-example-schema))
:   List of filters that can be applied to the dashboard's data. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-filters=@path/to/file.json`.

`--dashboard-annotations` ([`ApisDashboardsV1AstAnnotation[]`](#cli-apis-dashboards-v1-ast-annotation-example-schema))
:   List of annotations that can be applied to the dashboard's visual elements. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-annotations=@path/to/file.json`.

`--dashboard-absolute-time-frame` ([`ApisDashboardsV1CommonTimeFrame`](#cli-apis-dashboards-v1-common-time-frame-example-schema))
:   Absolute time frame specifying a fixed start and end time. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-absolute-time-frame=@path/to/file.json`.

`--dashboard-relative-time-frame` (string)
:   Relative time frame specifying a duration from the current time. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `10` characters. The minimum length is `2` characters. The value must match regular expression `/^[0-9]+[smhdw]?$/`.

`--dashboard-folder-id` ([`ApisDashboardsV1UUID`](#cli-apis-dashboards-v1-uuid-example-schema))
:   Unique identifier of the folder containing the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-folder-id=@path/to/file.json`.

`--dashboard-folder-path` ([`ApisDashboardsV1AstFolderPath`](#cli-apis-dashboards-v1-ast-folder-path-example-schema))
:   Path of the folder containing the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-folder-path=@path/to/file.json`.

`--dashboard-false` ([`ApisDashboardsV1AstDashboardAutoRefreshOffEmpty`](#cli-apis-dashboards-v1-ast-dashboard-auto-refresh-off-empty-example-schema))
:   Auto refresh interval is set to off. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-false=@path/to/file.json`.

`--dashboard-two-minutes` ([`ApisDashboardsV1AstDashboardAutoRefreshTwoMinutesEmpty`](#cli-apis-dashboards-v1-ast-dashboard-auto-refresh-two-minutes-empty-example-schema))
:   Auto refresh interval is set to two minutes. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-two-minutes=@path/to/file.json`.

`--dashboard-five-minutes` ([`ApisDashboardsV1AstDashboardAutoRefreshFiveMinutesEmpty`](#cli-apis-dashboards-v1-ast-dashboard-auto-refresh-five-minutes-empty-example-schema))
:   Auto refresh interval is set to five minutes. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-five-minutes=@path/to/file.json`.

#### Examples
{: #cloud-logs-dashboard-create-examples}

```text
ibmcloud cloud-logs dashboard-create \
    --dashboard '{"href": "6U1Q8Hpa263Se8PkRKaiE", "id": "6U1Q8Hpa263Se8PkRKaiE", "name": "DataUsageToMetrics Dashboard", "description": "This dashboard shows the performance of our production environment.", "layout": {"sections": [{"href": "exampleString", "id": {"value": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "rows": [{"href": "exampleString", "id": {"value": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "appearance": {"height": 19}, "widgets": [{"href": "exampleString", "id": {"value": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "title": "Size", "description": "The average response time of the system", "definition": {"line_chart": {"legend": {"is_visible": true, "columns": ["unspecified","min","max","sum","avg","last","name"], "group_by_query": true}, "tooltip": {"show_labels": false, "type": "all"}, "query_definitions": [{"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "query": {"metrics": {"promql_query": {"value": "sum(rate(cx_data_usage_bytes_total[20m]))by(pillar,tier)"}, "filters": [{"label": "service", "operator": {"equals": {"selection": {"all": {}}}}}]}}, "series_name_template": "{{severity}}", "series_count_limit": "20", "unit": "usd", "scale_type": "linear", "name": "Query1", "is_visible": true, "color_scheme": "classic", "resolution": {"interval": "1m", "buckets_presented": 96}, "data_mode_type": "archive"}], "stacked_line": "relative"}}, "created_at": "2021-01-01T00:00:00.000Z", "updated_at": "2021-01-01T00:00:00.000Z"}]}]}]}, "variables": [{"name": "service_name", "definition": {"multi_select": {"source": {"logs_path": {"observation_field": {"keypath": ["applicationname"], "scope": "metadata"}}}, "selection": {"all": {}}, "values_order_direction": "desc"}}, "display_name": "Service Name"}], "filters": [{"source": {"logs": {"operator": {"equals": {"selection": {"all": {}}}}, "observation_field": {"keypath": ["applicationname"], "scope": "metadata"}}}, "enabled": true, "collapsed": false}], "annotations": [{"href": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "name": "Deployments", "enabled": true, "source": {"metrics": {"promql_query": {"value": "sum(up)"}, "strategy": {"start_time_metric": {}}, "message_template": "exampleString", "labels": ["exampleString","anotherTestString"]}}}], "relative_time_frame": "86400s"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs dashboard-create \
    --dashboard-href 6U1Q8Hpa263Se8PkRKaiE \
    --dashboard-id 6U1Q8Hpa263Se8PkRKaiE \
    --dashboard-name 'My Dashboard' \
    --dashboard-description 'This dashboard shows the performance of our production environment.' \
    --dashboard-layout apisDashboardsV1AstLayout \
    --dashboard-variables '[apisDashboardsV1AstVariable]' \
    --dashboard-filters '[apisDashboardsV1AstFilter]' \
    --dashboard-annotations '[apisDashboardsV1AstAnnotation]' \
    --dashboard-relative-time-frame 1d
```
{: pre}

### `ibmcloud cloud-logs dashboard`
{: #cloud-logs-cli-dashboard-command}

Gets an existing dashboard.

```text
ibmcloud cloud-logs dashboard --dashboard-id DASHBOARD-ID
```


#### Command options
{: #cloud-logs-dashboard-cli-options}

`--dashboard-id` (string)
:   The ID of the dashboard. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-dashboard-examples}

```text
ibmcloud cloud-logs dashboard \
    --dashboard-id exampleString
```
{: pre}

### `ibmcloud cloud-logs dashboard-replace`
{: #cloud-logs-cli-dashboard-replace-command}

Replaces an existing dashboard.

```text
ibmcloud cloud-logs dashboard-replace --dashboard-id DASHBOARD-ID [--dashboard DASHBOARD | --dashboard-href DASHBOARD-HREF --dashboard-name DASHBOARD-NAME --dashboard-description DASHBOARD-DESCRIPTION --dashboard-layout DASHBOARD-LAYOUT --dashboard-variables DASHBOARD-VARIABLES --dashboard-filters DASHBOARD-FILTERS --dashboard-annotations DASHBOARD-ANNOTATIONS --dashboard-absolute-time-frame DASHBOARD-ABSOLUTE-TIME-FRAME --dashboard-relative-time-frame DASHBOARD-RELATIVE-TIME-FRAME --dashboard-folder-id DASHBOARD-FOLDER-ID --dashboard-folder-path DASHBOARD-FOLDER-PATH --dashboard-false DASHBOARD-FALSE --dashboard-two-minutes DASHBOARD-TWO-MINUTES --dashboard-five-minutes DASHBOARD-FIVE-MINUTES]
```


#### Command options
{: #cloud-logs-dashboard-replace-cli-options}

`--dashboard-id` (string)
:   The ID of the dashboard. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--dashboard` ([`Dashboard`](#cli-dashboard-example-schema))
:   Dashboard represents the structure and configuration of a Coralogix Custom Dashboard. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard=@path/to/file.json`.

`--dashboard-href` (string)
:   Unique identifier for the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `21` characters. The minimum length is `21` characters. The value must match regular expression `/^[a-zA-Z0-9]{21}$/`.

`--dashboard-name` (string)
:   Display name of the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--dashboard-description` (string)
:   Brief description or summary of the dashboard's purpose or content. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `200` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--dashboard-layout` ([`ApisDashboardsV1AstLayout`](#cli-apis-dashboards-v1-ast-layout-example-schema))
:   Layout configuration for the dashboard's visual elements. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-layout=@path/to/file.json`.

`--dashboard-variables` ([`ApisDashboardsV1AstVariable[]`](#cli-apis-dashboards-v1-ast-variable-example-schema))
:   List of variables that can be used within the dashboard for dynamic content. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-variables=@path/to/file.json`.

`--dashboard-filters` ([`ApisDashboardsV1AstFilter[]`](#cli-apis-dashboards-v1-ast-filter-example-schema))
:   List of filters that can be applied to the dashboard's data. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-filters=@path/to/file.json`.

`--dashboard-annotations` ([`ApisDashboardsV1AstAnnotation[]`](#cli-apis-dashboards-v1-ast-annotation-example-schema))
:   List of annotations that can be applied to the dashboard's visual elements. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-annotations=@path/to/file.json`.

`--dashboard-absolute-time-frame` ([`ApisDashboardsV1CommonTimeFrame`](#cli-apis-dashboards-v1-common-time-frame-example-schema))
:   Absolute time frame specifying a fixed start and end time. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-absolute-time-frame=@path/to/file.json`.

`--dashboard-relative-time-frame` (string)
:   Relative time frame specifying a duration from the current time. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    The maximum length is `10` characters. The minimum length is `2` characters. The value must match regular expression `/^[0-9]+[smhdw]?$/`.

`--dashboard-folder-id` ([`ApisDashboardsV1UUID`](#cli-apis-dashboards-v1-uuid-example-schema))
:   Unique identifier of the folder containing the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-folder-id=@path/to/file.json`.

`--dashboard-folder-path` ([`ApisDashboardsV1AstFolderPath`](#cli-apis-dashboards-v1-ast-folder-path-example-schema))
:   Path of the folder containing the dashboard. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-folder-path=@path/to/file.json`.

`--dashboard-false` ([`ApisDashboardsV1AstDashboardAutoRefreshOffEmpty`](#cli-apis-dashboards-v1-ast-dashboard-auto-refresh-off-empty-example-schema))
:   Auto refresh interval is set to off. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-false=@path/to/file.json`.

`--dashboard-two-minutes` ([`ApisDashboardsV1AstDashboardAutoRefreshTwoMinutesEmpty`](#cli-apis-dashboards-v1-ast-dashboard-auto-refresh-two-minutes-empty-example-schema))
:   Auto refresh interval is set to two minutes. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-two-minutes=@path/to/file.json`.

`--dashboard-five-minutes` ([`ApisDashboardsV1AstDashboardAutoRefreshFiveMinutesEmpty`](#cli-apis-dashboards-v1-ast-dashboard-auto-refresh-five-minutes-empty-example-schema))
:   Auto refresh interval is set to five minutes. This option provides a value for a sub-field of the JSON option 'dashboard'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--dashboard-five-minutes=@path/to/file.json`.

#### Examples
{: #cloud-logs-dashboard-replace-examples}

```text
ibmcloud cloud-logs dashboard-replace \
    --dashboard-id exampleString \
    --dashboard '{"href": "6U1Q8Hpa263Se8PkRKaiE", "id": "6U1Q8Hpa263Se8PkRKaiE", "name": "DataUsageToMetrics Dashboard", "description": "This dashboard shows the performance of our production environment.", "layout": {"sections": [{"href": "exampleString", "id": {"value": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "rows": [{"href": "exampleString", "id": {"value": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "appearance": {"height": 19}, "widgets": [{"href": "exampleString", "id": {"value": "9fab83da-98cb-4f18-a7ba-b6f0435c9673"}, "title": "Size", "description": "The average response time of the system", "definition": {"line_chart": {"legend": {"is_visible": true, "columns": ["unspecified","min","max","sum","avg","last","name"], "group_by_query": true}, "tooltip": {"show_labels": false, "type": "all"}, "query_definitions": [{"id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "query": {"metrics": {"promql_query": {"value": "sum(rate(cx_data_usage_bytes_total[20m]))by(pillar,tier)"}, "filters": [{"label": "service", "operator": {"equals": {"selection": {"all": {}}}}}]}}, "series_name_template": "{{severity}}", "series_count_limit": "20", "unit": "usd", "scale_type": "linear", "name": "Query1", "is_visible": true, "color_scheme": "classic", "resolution": {"interval": "1m", "buckets_presented": 96}, "data_mode_type": "archive"}], "stacked_line": "relative"}}, "created_at": "2021-01-01T00:00:00.000Z", "updated_at": "2021-01-01T00:00:00.000Z"}]}]}]}, "variables": [{"name": "service_name", "definition": {"multi_select": {"source": {"logs_path": {"observation_field": {"keypath": ["applicationname"], "scope": "metadata"}}}, "selection": {"all": {}}, "values_order_direction": "desc"}}, "display_name": "Service Name"}], "filters": [{"source": {"logs": {"operator": {"equals": {"selection": {"all": {}}}}, "observation_field": {"keypath": ["applicationname"], "scope": "metadata"}}}, "enabled": true, "collapsed": false}], "annotations": [{"href": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "id": "9fab83da-98cb-4f18-a7ba-b6f0435c9673", "name": "Deployments", "enabled": true, "source": {"metrics": {"promql_query": {"value": "sum(up)"}, "strategy": {"start_time_metric": {}}, "message_template": "exampleString", "labels": ["exampleString","anotherTestString"]}}}], "relative_time_frame": "86400s"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs dashboard-replace \
    --dashboard-id exampleString \
    --dashboard-href 6U1Q8Hpa263Se8PkRKaiE \
    --dashboard-name 'My Dashboard' \
    --dashboard-description 'This dashboard shows the performance of our production environment.' \
    --dashboard-layout apisDashboardsV1AstLayout \
    --dashboard-variables '[apisDashboardsV1AstVariable]' \
    --dashboard-filters '[apisDashboardsV1AstFilter]' \
    --dashboard-annotations '[apisDashboardsV1AstAnnotation]' \
    --dashboard-relative-time-frame 1d
```
{: pre}

### `ibmcloud cloud-logs dashboard-delete`
{: #cloud-logs-cli-dashboard-delete-command}

Deletes an existing dashboard.

```text
ibmcloud cloud-logs dashboard-delete --dashboard-id DASHBOARD-ID
```


#### Command options
{: #cloud-logs-dashboard-delete-cli-options}

`--dashboard-id` (string)
:   The ID of the dashboard. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-dashboard-delete-examples}

```text
ibmcloud cloud-logs dashboard-delete \
    --dashboard-id exampleString
```
{: pre}

### `ibmcloud cloud-logs pin-dashboard`
{: #cloud-logs-cli-pin-dashboard-command}

Add dashboard to the favorite folder.

```text
ibmcloud cloud-logs pin-dashboard --dashboard-id DASHBOARD-ID
```


#### Command options
{: #cloud-logs-pin-dashboard-cli-options}

`--dashboard-id` (string)
:   The ID of the dashboard. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-pin-dashboard-examples}

```text
ibmcloud cloud-logs pin-dashboard \
    --dashboard-id exampleString
```
{: pre}

### `ibmcloud cloud-logs unpin-dashboard`
{: #cloud-logs-cli-unpin-dashboard-command}

Remove dashboard to the favorite folder.

```text
ibmcloud cloud-logs unpin-dashboard --dashboard-id DASHBOARD-ID
```


#### Command options
{: #cloud-logs-unpin-dashboard-cli-options}

`--dashboard-id` (string)
:   The ID of the dashboard. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-unpin-dashboard-examples}

```text
ibmcloud cloud-logs unpin-dashboard \
    --dashboard-id exampleString
```
{: pre}

### `ibmcloud cloud-logs default-dashboard-replace`
{: #cloud-logs-cli-default-dashboard-replace-command}

Set dashboard as the default dashboard for the user.

```text
ibmcloud cloud-logs default-dashboard-replace --dashboard-id DASHBOARD-ID
```


#### Command options
{: #cloud-logs-default-dashboard-replace-cli-options}

`--dashboard-id` (string)
:   The ID of the dashboard. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-default-dashboard-replace-examples}

```text
ibmcloud cloud-logs default-dashboard-replace \
    --dashboard-id exampleString
```
{: pre}

### `ibmcloud cloud-logs assign-dashboard-folder`
{: #cloud-logs-cli-assign-dashboard-folder-command}

Assign a dashboard to a folder.

```text
ibmcloud cloud-logs assign-dashboard-folder --dashboard-id DASHBOARD-ID --folder-id FOLDER-ID
```


#### Command options
{: #cloud-logs-assign-dashboard-folder-cli-options}

`--dashboard-id` (string)
:   The ID of the dashboard. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--folder-id` (string)
:   The folder ID could be null to assign the dashboard to root. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-assign-dashboard-folder-examples}

```text
ibmcloud cloud-logs assign-dashboard-folder \
    --dashboard-id exampleString \
    --folder-id exampleString
```
{: pre}

## DashboardFoldersService
{: #cloud-logs-dashboard-folders-service-cli}

API to manage your dashboard folders.

### `ibmcloud cloud-logs dashboard-folders`
{: #cloud-logs-cli-dashboard-folders-command}

List all dashboard folders.

```text
ibmcloud cloud-logs dashboard-folders
```


#### Example
{: #cloud-logs-dashboard-folders-examples}

```text
ibmcloud cloud-logs dashboard-folders
```
{: pre}

### `ibmcloud cloud-logs dashboard-folder-create`
{: #cloud-logs-cli-dashboard-folder-create-command}

Create a dashboard folder.

```text
ibmcloud cloud-logs dashboard-folder-create --name NAME [--id ID] [--parent-id PARENT-ID]
```


#### Command options
{: #cloud-logs-dashboard-folder-create-cli-options}

`--name` (string)
:   The dashboard folder name, required. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--id` (strfmt.UUID)
:   The dashboard folder ID, uuid.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--parent-id` (strfmt.UUID)
:   The dashboard folder parent ID, optional. If not set, the folder is a root
 folder, if set, the folder is a subfolder of the parent folder and needs to
 be a uuid.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-dashboard-folder-create-examples}

```text
ibmcloud cloud-logs dashboard-folder-create \
    --name 'My Folder' \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --parent-id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs dashboard-folder-replace`
{: #cloud-logs-cli-dashboard-folder-replace-command}

Update a dashboard folder.

```text
ibmcloud cloud-logs dashboard-folder-replace --folder-id FOLDER-ID --name NAME [--id ID] [--parent-id PARENT-ID]
```


#### Command options
{: #cloud-logs-dashboard-folder-replace-cli-options}

`--folder-id` (strfmt.UUID)
:   The folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--name` (string)
:   The dashboard folder name, required. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--id` (strfmt.UUID)
:   The dashboard folder ID, uuid.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--parent-id` (strfmt.UUID)
:   The dashboard folder parent ID, optional. If not set, the folder is a root
 folder, if set, the folder is a subfolder of the parent folder and needs to
 be a uuid.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-dashboard-folder-replace-examples}

```text
ibmcloud cloud-logs dashboard-folder-replace \
    --folder-id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'My Folder' \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --parent-id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs dashboard-folder-delete`
{: #cloud-logs-cli-dashboard-folder-delete-command}

Delete a dashboard folder.

```text
ibmcloud cloud-logs dashboard-folder-delete --folder-id FOLDER-ID
```


#### Command options
{: #cloud-logs-dashboard-folder-delete-cli-options}

`--folder-id` (strfmt.UUID)
:   The folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-dashboard-folder-delete-examples}

```text
ibmcloud cloud-logs dashboard-folder-delete \
    --folder-id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

## Events2MetricService
{: #cloud-logs-events2-metric-service-cli}

Create and manage your events to metrics definitions.

### `ibmcloud cloud-logs events2metrics-list`
{: #cloud-logs-cli-events2metrics-list-command}

Lists event to metrics definitions.

```text
ibmcloud cloud-logs events2metrics-list
```


#### Example
{: #cloud-logs-events2metrics-list-examples}

```text
ibmcloud cloud-logs events2metrics-list
```
{: pre}

### `ibmcloud cloud-logs events2metrics-create`
{: #cloud-logs-cli-events2metrics-create-command}

Creates event to metrics definitions.

```text
ibmcloud cloud-logs events2metrics-create [--event2-metric-prototype EVENT2-METRIC-PROTOTYPE | --event2-metric-name EVENT2-METRIC-NAME --event2-metric-description EVENT2-METRIC-DESCRIPTION --event2-metric-permutations-limit EVENT2-METRIC-PERMUTATIONS-LIMIT --event2-metric-metric-labels EVENT2-METRIC-METRIC-LABELS --event2-metric-metric-fields EVENT2-METRIC-METRIC-FIELDS --event2-metric-type EVENT2-METRIC-TYPE --event2-metric-logs-query EVENT2-METRIC-LOGS-QUERY]
```


#### Command options
{: #cloud-logs-events2metrics-create-cli-options}

`--event2-metric-prototype` ([`Event2MetricPrototype`](#cli-event2-metric-prototype-example-schema))
:   E2M Create message. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-prototype=@path/to/file.json`.

`--event2-metric-name` (string)
:   Name of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--event2-metric-description` (string)
:   Description of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--event2-metric-permutations-limit` (int64)
:   The permutation limit of the E2M. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

`--event2-metric-metric-labels` ([`ApisEvents2metricsV2MetricLabel[]`](#cli-apis-events2metrics-v2-metric-label-example-schema))
:   E2M metric labels. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-labels=@path/to/file.json`.

`--event2-metric-metric-fields` ([`ApisEvents2metricsV2MetricField[]`](#cli-apis-events2metrics-v2-metric-field-example-schema))
:   E2M metric fields. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-fields=@path/to/file.json`.

`--event2-metric-type` (string)
:   E2M type. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `logs2metrics`.

`--event2-metric-logs-query` ([`ApisLogs2metricsV2LogsQuery`](#cli-apis-logs2metrics-v2-logs-query-example-schema))
:   E2M logs query. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-logs-query=@path/to/file.json`.

#### Examples
{: #cloud-logs-events2metrics-create-examples}

```text
ibmcloud cloud-logs events2metrics-create \
    --event2-metric-prototype '{"name": "test em2", "description": "Test e2m", "permutations_limit": 1, "metric_labels": [{"target_label": "alias_label_name", "source_field": "log_obj.string_value"}], "metric_fields": [{"target_base_metric_name": "alias_field_name", "source_field": "log_obj.numeric_field", "aggregations": [{"enabled": true, "agg_type": "samples", "target_metric_name": "alias_field_name_agg_func", "samples": {"sample_type": "max"}}]}], "type": "logs2metrics", "logs_query": {"lucene": "logs", "alias": "new_query", "applicationname_filters": ["app_name"], "subsystemname_filters": ["sub_name"], "severity_filters": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs events2metrics-create \
    --event2-metric-name 'Service catalog latency' \
    --event2-metric-description 'avg and max the latency of catalog service' \
    --event2-metric-permutations-limit 30000 \
    --event2-metric-metric-labels '[apisEvents2metricsV2MetricLabel]' \
    --event2-metric-metric-fields '[apisEvents2metricsV2MetricField]' \
    --event2-metric-type logs2metrics \
    --event2-metric-logs-query apisLogs2metricsV2LogsQuery
```
{: pre}

### `ibmcloud cloud-logs events2metrics`
{: #cloud-logs-cli-events2metrics-command}

Gets event to metrics definitions by id.

```text
ibmcloud cloud-logs events2metrics --id ID
```


#### Command options
{: #cloud-logs-events2metrics-cli-options}

`--id` (string)
:   ID of e2m to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-events2metrics-examples}

```text
ibmcloud cloud-logs events2metrics \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09
```
{: pre}

### `ibmcloud cloud-logs events2metrics-replace`
{: #cloud-logs-cli-events2metrics-replace-command}

Updates event to metrics definitions.

```text
ibmcloud cloud-logs events2metrics-replace --id ID [--event2-metric-prototype EVENT2-METRIC-PROTOTYPE | --event2-metric-name EVENT2-METRIC-NAME --event2-metric-description EVENT2-METRIC-DESCRIPTION --event2-metric-permutations-limit EVENT2-METRIC-PERMUTATIONS-LIMIT --event2-metric-metric-labels EVENT2-METRIC-METRIC-LABELS --event2-metric-metric-fields EVENT2-METRIC-METRIC-FIELDS --event2-metric-type EVENT2-METRIC-TYPE --event2-metric-logs-query EVENT2-METRIC-LOGS-QUERY]
```


#### Command options
{: #cloud-logs-events2metrics-replace-cli-options}

`--id` (string)
:   ID of e2m to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--event2-metric-prototype` ([`Event2MetricPrototype`](#cli-event2-metric-prototype-example-schema))
:   E2M Create message. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-prototype=@path/to/file.json`.

`--event2-metric-name` (string)
:   Name of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--event2-metric-description` (string)
:   Description of E2M to create. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\-\\s]+$/`.

`--event2-metric-permutations-limit` (int64)
:   The permutation limit of the E2M. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

`--event2-metric-metric-labels` ([`ApisEvents2metricsV2MetricLabel[]`](#cli-apis-events2metrics-v2-metric-label-example-schema))
:   E2M metric labels. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-labels=@path/to/file.json`.

`--event2-metric-metric-fields` ([`ApisEvents2metricsV2MetricField[]`](#cli-apis-events2metrics-v2-metric-field-example-schema))
:   E2M metric fields. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-metric-fields=@path/to/file.json`.

`--event2-metric-type` (string)
:   E2M type. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `logs2metrics`.

`--event2-metric-logs-query` ([`ApisLogs2metricsV2LogsQuery`](#cli-apis-logs2metrics-v2-logs-query-example-schema))
:   E2M logs query. This option provides a value for a sub-field of the JSON option 'event2-metric-prototype'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--event2-metric-logs-query=@path/to/file.json`.

#### Examples
{: #cloud-logs-events2metrics-replace-examples}

```text
ibmcloud cloud-logs events2metrics-replace \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09 \
    --event2-metric-prototype '{"name": "test em2", "description": "Test e2m updated", "permutations_limit": 1, "metric_labels": [{"target_label": "alias_label_name", "source_field": "log_obj.string_value"}], "metric_fields": [{"target_base_metric_name": "alias_field_name", "source_field": "log_obj.numeric_field", "aggregations": [{"enabled": true, "agg_type": "samples", "target_metric_name": "alias_field_name_agg_func", "samples": {"sample_type": "max"}}]}], "type": "logs2metrics", "logs_query": {"lucene": "logs", "alias": "new_query", "applicationname_filters": ["app_name"], "subsystemname_filters": ["sub_name"], "severity_filters": ["unspecified","debug","verbose","info","warning","error","critical"]}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs events2metrics-replace \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09 \
    --event2-metric-name 'Service catalog latency' \
    --event2-metric-description 'avg and max the latency of catalog service' \
    --event2-metric-permutations-limit 30000 \
    --event2-metric-metric-labels '[apisEvents2metricsV2MetricLabel]' \
    --event2-metric-metric-fields '[apisEvents2metricsV2MetricField]' \
    --event2-metric-type logs2metrics \
    --event2-metric-logs-query apisLogs2metricsV2LogsQuery
```
{: pre}

### `ibmcloud cloud-logs events2metrics-delete`
{: #cloud-logs-cli-events2metrics-delete-command}

Deletes event to metrics definitions by id.

```text
ibmcloud cloud-logs events2metrics-delete --id ID
```


#### Command options
{: #cloud-logs-events2metrics-delete-cli-options}

`--id` (string)
:   ID of e2m to be deleted. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-events2metrics-delete-examples}

```text
ibmcloud cloud-logs events2metrics-delete \
    --id d6a3658e-78d2-47d0-9b81-b2c551f01b09
```
{: pre}

## ViewsService
{: #cloud-logs-views-service-cli}

Create and manage views.

### `ibmcloud cloud-logs views`
{: #cloud-logs-cli-views-command}

Lists all company public views.

```text
ibmcloud cloud-logs views
```


#### Example
{: #cloud-logs-views-examples}

```text
ibmcloud cloud-logs views
```
{: pre}

### `ibmcloud cloud-logs view-create`
{: #cloud-logs-cli-view-create-command}

Creates a new view.

```text
ibmcloud cloud-logs view-create --name NAME [--search-query SEARCH-QUERY | --search-query-query SEARCH-QUERY-QUERY] [--time-selection TIME-SELECTION | --time-selection-quick-selection TIME-SELECTION-QUICK-SELECTION --time-selection-custom-selection TIME-SELECTION-CUSTOM-SELECTION] [--filters FILTERS | --filters-filters FILTERS-FILTERS] [--folder-id FOLDER-ID]
```


#### Command options
{: #cloud-logs-view-create-cli-options}

`--name` (string)
:   View name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--search-query` ([`ApisViewsV1SearchQuery`](#cli-apis-views-v1-search-query-example-schema))
:   View search query. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--search-query=@path/to/file.json`.

`--time-selection` ([`ApisViewsV1TimeSelection`](#cli-apis-views-v1-time-selection-example-schema))
:   View time selection. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection=@path/to/file.json`.

`--filters` ([`ApisViewsV1SelectedFilters`](#cli-apis-views-v1-selected-filters-example-schema))
:   View selected filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--folder-id` (strfmt.UUID)
:   View folder ID.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--search-query-query` (string)
:   View search query. This option provides a value for a sub-field of the JSON option 'search-query'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--time-selection-quick-selection` ([`ApisViewsV1QuickTimeSelection`](#cli-apis-views-v1-quick-time-selection-example-schema))
:   Quick time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-quick-selection=@path/to/file.json`.

`--time-selection-custom-selection` ([`ApisViewsV1CustomTimeSelection`](#cli-apis-views-v1-custom-time-selection-example-schema))
:   Custom time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-custom-selection=@path/to/file.json`.

`--filters-filters` ([`ApisViewsV1Filter[]`](#cli-apis-views-v1-filter-example-schema))
:   Selected filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-filters=@path/to/file.json`.

#### Examples
{: #cloud-logs-view-create-examples}

```text
ibmcloud cloud-logs view-create \
    --name 'Logs view' \
    --search-query '{"query": "logs"}' \
    --time-selection '{"custom_selection": {"from_time": "2024-01-25T11:31:43.152Z", "to_time": "2024-01-25T11:37:13.238Z"}}' \
    --filters '{"filters": [{"name": "applicationName", "selected_values": {}}]}' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs view-create \
    --name 'Logs view' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --search-query-query error \
    --time-selection-custom-selection apisViewsV1CustomTimeSelection \
    --filters-filters '[apisViewsV1Filter]'
```
{: pre}

### `ibmcloud cloud-logs view`
{: #cloud-logs-cli-view-command}

Gets a view by ID.

```text
ibmcloud cloud-logs view --id ID
```


#### Command options
{: #cloud-logs-view-cli-options}

`--id` (int64)
:   View ID. Required.

#### Example
{: #cloud-logs-view-examples}

```text
ibmcloud cloud-logs view \
    --id 52
```
{: pre}

### `ibmcloud cloud-logs view-replace`
{: #cloud-logs-cli-view-replace-command}

Replaces an existing view.

```text
ibmcloud cloud-logs view-replace --id ID --name NAME [--search-query SEARCH-QUERY | --search-query-query SEARCH-QUERY-QUERY] [--time-selection TIME-SELECTION | --time-selection-quick-selection TIME-SELECTION-QUICK-SELECTION --time-selection-custom-selection TIME-SELECTION-CUSTOM-SELECTION] [--filters FILTERS | --filters-filters FILTERS-FILTERS] [--folder-id FOLDER-ID]
```


#### Command options
{: #cloud-logs-view-replace-cli-options}

`--id` (int64)
:   View ID. Required.

`--name` (string)
:   View name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--search-query` ([`ApisViewsV1SearchQuery`](#cli-apis-views-v1-search-query-example-schema))
:   View search query. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--search-query=@path/to/file.json`.

`--time-selection` ([`ApisViewsV1TimeSelection`](#cli-apis-views-v1-time-selection-example-schema))
:   View time selection. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection=@path/to/file.json`.

`--filters` ([`ApisViewsV1SelectedFilters`](#cli-apis-views-v1-selected-filters-example-schema))
:   View selected filters. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters=@path/to/file.json`.

`--folder-id` (strfmt.UUID)
:   View folder ID.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--search-query-query` (string)
:   View search query. This option provides a value for a sub-field of the JSON option 'search-query'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--time-selection-quick-selection` ([`ApisViewsV1QuickTimeSelection`](#cli-apis-views-v1-quick-time-selection-example-schema))
:   Quick time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-quick-selection=@path/to/file.json`.

`--time-selection-custom-selection` ([`ApisViewsV1CustomTimeSelection`](#cli-apis-views-v1-custom-time-selection-example-schema))
:   Custom time selection. This option provides a value for a sub-field of the JSON option 'time-selection'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--time-selection-custom-selection=@path/to/file.json`.

`--filters-filters` ([`ApisViewsV1Filter[]`](#cli-apis-views-v1-filter-example-schema))
:   Selected filters. This option provides a value for a sub-field of the JSON option 'filters'. It is mutually exclusive with that option.

    The maximum length is `4096` items. The minimum length is `1` item.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--filters-filters=@path/to/file.json`.

#### Examples
{: #cloud-logs-view-replace-examples}

```text
ibmcloud cloud-logs view-replace \
    --id 52 \
    --name 'Logs view' \
    --search-query '{"query": "logs new"}' \
    --time-selection '{"custom_selection": {"from_time": "2024-01-25T11:31:43.152Z", "to_time": "2024-01-25T11:37:13.238Z"}}' \
    --filters '{"filters": [{"name": "applicationName", "selected_values": {}}]}' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs view-replace \
    --id 52 \
    --name 'Logs view' \
    --folder-id 9fab83da-98cb-4f18-a7ba-b6f0435c9673 \
    --search-query-query error \
    --time-selection-custom-selection apisViewsV1CustomTimeSelection \
    --filters-filters '[apisViewsV1Filter]'
```
{: pre}

### `ibmcloud cloud-logs view-delete`
{: #cloud-logs-cli-view-delete-command}

Deletes a view by ID.

```text
ibmcloud cloud-logs view-delete --id ID
```


#### Command options
{: #cloud-logs-view-delete-cli-options}

`--id` (int64)
:   View ID. Required.

#### Example
{: #cloud-logs-view-delete-examples}

```text
ibmcloud cloud-logs view-delete \
    --id 52
```
{: pre}

## ViewsFoldersService
{: #cloud-logs-views-folders-service-cli}

Create and manage view folders.

### `ibmcloud cloud-logs view-folders`
{: #cloud-logs-cli-view-folders-command}

List view's folders.

```text
ibmcloud cloud-logs view-folders
```


#### Example
{: #cloud-logs-view-folders-examples}

```text
ibmcloud cloud-logs view-folders
```
{: pre}

### `ibmcloud cloud-logs view-folder-create`
{: #cloud-logs-cli-view-folder-create-command}

Create view folder.

```text
ibmcloud cloud-logs view-folder-create --name NAME
```


#### Command options
{: #cloud-logs-view-folder-create-cli-options}

`--name` (string)
:   View folder name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-view-folder-create-examples}

```text
ibmcloud cloud-logs view-folder-create \
    --name 'My Folder'
```
{: pre}

### `ibmcloud cloud-logs view-folder`
{: #cloud-logs-cli-view-folder-command}

Get view folder.

```text
ibmcloud cloud-logs view-folder --id ID
```


#### Command options
{: #cloud-logs-view-folder-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-view-folder-examples}

```text
ibmcloud cloud-logs view-folder \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

### `ibmcloud cloud-logs view-folder-replace`
{: #cloud-logs-cli-view-folder-replace-command}

Replaces an existing view folder.

```text
ibmcloud cloud-logs view-folder-replace --id ID --name NAME
```


#### Command options
{: #cloud-logs-view-folder-replace-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

`--name` (string)
:   View folder name. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

#### Example
{: #cloud-logs-view-folder-replace-examples}

```text
ibmcloud cloud-logs view-folder-replace \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f \
    --name 'My Folder'
```
{: pre}

### `ibmcloud cloud-logs view-folder-delete`
{: #cloud-logs-cli-view-folder-delete-command}

Deletes a view folder by ID.

```text
ibmcloud cloud-logs view-folder-delete --id ID
```


#### Command options
{: #cloud-logs-view-folder-delete-cli-options}

`--id` (strfmt.UUID)
:   Folder ID. Required.

    The maximum length is `36` characters. The minimum length is `36` characters. The value must match regular expression `/^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/`.

#### Example
{: #cloud-logs-view-folder-delete-examples}

```text
ibmcloud cloud-logs view-folder-delete \
    --id 3dc02998-0b50-4ea8-b68a-4779d716fa1f
```
{: pre}

## QueryService
{: #cloud-logs-query-service-cli}

Query and process your logs.

### `ibmcloud cloud-logs query`
{: #cloud-logs-cli-query-command}

Run a query to search the logs.

```text
ibmcloud cloud-logs query --query QUERY [--metadata METADATA | --metadata-start-date METADATA-START-DATE --metadata-end-date METADATA-END-DATE --metadata-default-source METADATA-DEFAULT-SOURCE --metadata-tier METADATA-TIER --metadata-syntax METADATA-SYNTAX --metadata-limit METADATA-LIMIT --metadata-strict-fields-validation METADATA-STRICT-FIELDS-VALIDATION] [--since SINCE] [--local-time LOCAL-TIME]
```

#### Command options
{: #cloud-logs-query-cli-options}

`--query` (string)
:   The query for which you are seeking results. Required.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--metadata` ([`ApisDataprimeV1Metadata`](#cli-apis-dataprime-v1-metadata-example-schema))
:   Configuration for query execution. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--metadata=@path/to/file.json`.

`--metadata-start-date` (strfmt.DateTime)
:   Beginning of the time range for the query. Default: end - 15 min or current time - 15 min if end is not defined. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-end-date` (strfmt.DateTime)
:   End of the time range for the query. Default: start + 15 min or current time if start is not defined. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-default-source` (string)
:   Default value for the source to be used when the source is omitted in a query. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

    The maximum length is `4096` characters. The minimum length is `1` character. The value must match regular expression `/^[A-Za-z0-9_\\.,\\-"{}()\\[\\]=!:#\/$|' ]+$/`.

`--metadata-tier` (string)
:   Tier on which the query runs. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `archive`, `frequent_search`.

`--metadata-syntax` (string)
:   The syntax in which the query is written. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

    Allowable values are: `unspecified`, `lucene`, `dataprime`.

`--metadata-limit` (int64)
:   Limit the number of results. Default: 2000; max for TIER_FREQUENT_SEARCH: 12000; max for TIER_ARCHIVE: 50000. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-strict-fields-validation` (bool)
:   Prohibit the use of unknown fields, i.e., those not detected in the ingested data. Default: false. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--since` (duration)
: Query lookback window. Default 1h. Using this flag overrides metadata-start-date and metadata-end-date.

`--local-time` (bool)
: Converts the timestamp of the logs to local time.

#### Examples
{: #cloud-logs-query-examples}

```text
ibmcloud cloud-logs query \
    --query 'source logs | filter $d.apiVersion == 42' \
    --metadata '{"start_date": "2021-01-01T00:00:00.000Z", "end_date": "2021-01-01T00:00:00.000Z", "default_source": "logs", "tier": "frequent_search", "syntax": "dataprime", "limit": 2000, "strict_fields_validation": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```text
ibmcloud cloud-logs query \
    --query 'source logs | filter $d.apiVersion == 42' \
    --metadata-start-date 2021-01-01T00:00:00.000Z \
    --metadata-end-date 2021-01-01T00:00:00.000Z \
    --metadata-default-source logs \
    --metadata-tier frequent_search \
    --metadata-syntax dataprime \
    --metadata-limit 2000 \
    --metadata-strict-fields-validation true
```
{: pre}

## Schema examples
{: #cloud-logs-schema-examples}

The following schema examples represent the data that you need to specify for a command option. These examples model the data structure and include placeholder values for the expected value type. When you run a command, replace these values with the values that apply to your environment as appropriate.

### AlertsV1AlertActiveWhen
{: #cli-alerts-v1-alert-active-when-example-schema}

The following example shows the format of the AlertsV1AlertActiveWhen object.

```json

{
  "timeframes" : [ {
    "days_of_week" : [ "monday_or_unspecified", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday" ],
    "range" : {
      "start" : {
        "hours" : 18,
        "minutes" : 30,
        "seconds" : 0
      },
      "end" : {
        "hours" : 18,
        "minutes" : 30,
        "seconds" : 0
      }
    }
  } ]
}
```
{: codeblock}

### AlertsV1Date
{: #cli-alerts-v1-date-example-schema}

The following example shows the format of the AlertsV1Date object.

```json

{
  "year" : 2012,
  "month" : 12,
  "day" : 24
}
```
{: codeblock}

### AlertsV1MetaLabel[]
{: #cli-alerts-v1-meta-label-example-schema}

The following example shows the format of the AlertsV1MetaLabel[] object.

```json

[ {
  "key" : "env",
  "value" : "dev"
} ]
```
{: codeblock}

### AlertsV2AlertIncidentSettings
{: #cli-alerts-v2-alert-incident-settings-example-schema}

The following example shows the format of the AlertsV2AlertIncidentSettings object.

```json

{
  "retriggering_period_seconds" : 300,
  "notify_on" : "triggered_only",
  "use_as_notification_settings" : true
}
```
{: codeblock}

### AlertsV2AlertNotificationGroups[]
{: #cli-alerts-v2-alert-notification-groups-example-schema}

The following example shows the format of the AlertsV2AlertNotificationGroups[] object.

```json

[ {
  "group_by_fields" : [ "coralogix.metadata.applicationName" ],
  "notifications" : [ {
    "retriggering_period_seconds" : 60,
    "notify_on" : "triggered_and_resolved",
    "integration_id" : 123
  } ]
} ]
```
{: codeblock}

### ApisViewsV1SearchQuery
{: #cli-apis-views-v1-search-query-example-schema}

The following example shows the format of the ApisViewsV1SearchQuery object.

```json

{
  "query" : "logs"
}
```
{: codeblock}

### ApisViewsV1SelectedFilters
{: #cli-apis-views-v1-selected-filters-example-schema}

The following example shows the format of the ApisViewsV1SelectedFilters object.

```json

{
  "filters" : [ {
    "name" : "applicationName",
    "selected_values" : { }
  } ]
}
```
{: codeblock}

### ApisViewsV1TimeSelection
{: #cli-apis-views-v1-time-selection-example-schema}

The following example shows the format of the ApisViewsV1TimeSelection object.

```json

{
  "custom_selection" : {
    "from_time" : "2024-01-25T11:31:43.152Z",
    "to_time" : "2024-01-25T11:37:13.238Z"
  }
}
```
{: codeblock}

### Dashboard
{: #cli-dashboard-example-schema}

The following example shows the format of the Dashboard object.

```json

{
  "href" : "6U1Q8Hpa263Se8PkRKaiE",
  "id" : "6U1Q8Hpa263Se8PkRKaiE",
  "name" : "DataUsageToMetrics Dashboard",
  "description" : "This dashboard shows the performance of our production environment.",
  "layout" : {
    "sections" : [ {
      "href" : "exampleString",
      "id" : {
        "value" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
      },
      "rows" : [ {
        "href" : "exampleString",
        "id" : {
          "value" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
        },
        "appearance" : {
          "height" : 19
        },
        "widgets" : [ {
          "href" : "exampleString",
          "id" : {
            "value" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
          },
          "title" : "Size",
          "description" : "The average response time of the system",
          "definition" : {
            "line_chart" : {
              "legend" : {
                "is_visible" : true,
                "columns" : [ "unspecified", "min", "max", "sum", "avg", "last", "name" ],
                "group_by_query" : true
              },
              "tooltip" : {
                "show_labels" : false,
                "type" : "all"
              },
              "query_definitions" : [ {
                "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673",
                "query" : {
                  "metrics" : {
                    "promql_query" : {
                      "value" : "sum(rate(cx_data_usage_bytes_total[20m]))by(pillar,tier)"
                    },
                    "filters" : [ {
                      "label" : "service",
                      "operator" : {
                        "equals" : {
                          "selection" : {
                            "all" : { }
                          }
                        }
                      }
                    } ]
                  }
                },
                "series_name_template" : "{{severity}}",
                "series_count_limit" : "20",
                "unit" : "usd",
                "scale_type" : "linear",
                "name" : "Query1",
                "is_visible" : true,
                "color_scheme" : "classic",
                "resolution" : {
                  "interval" : "1m",
                  "buckets_presented" : 96
                },
                "data_mode_type" : "archive"
              } ],
              "stacked_line" : "relative"
            }
          },
          "created_at" : "2021-01-01T00:00:00.000Z",
          "updated_at" : "2021-01-01T00:00:00.000Z"
        } ]
      } ]
    } ]
  },
  "variables" : [ {
    "name" : "service_name",
    "definition" : {
      "multi_select" : {
        "source" : {
          "logs_path" : {
            "observation_field" : {
              "keypath" : [ "applicationname" ],
              "scope" : "metadata"
            }
          }
        },
        "selection" : {
          "all" : { }
        },
        "values_order_direction" : "desc"
      }
    },
    "display_name" : "Service Name"
  } ],
  "filters" : [ {
    "source" : {
      "logs" : {
        "operator" : {
          "equals" : {
            "selection" : {
              "all" : { }
            }
          }
        },
        "observation_field" : {
          "keypath" : [ "applicationname" ],
          "scope" : "metadata"
        }
      }
    },
    "enabled" : true,
    "collapsed" : false
  } ],
  "annotations" : [ {
    "href" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673",
    "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673",
    "name" : "Deployments",
    "enabled" : true,
    "source" : {
      "metrics" : {
        "promql_query" : {
          "value" : "sum(up)"
        },
        "strategy" : {
          "start_time_metric" : { }
        },
        "message_template" : "exampleString",
        "labels" : [ "exampleString", "anotherExampleString" ]
      }
    }
  } ],
  "relative_time_frame" : "86400s"
}
```
{: codeblock}

### Event2MetricPrototype
{: #cli-event2-metric-prototype-example-schema}

The following example shows the format of the Event2MetricPrototype object.

```json

{
  "name" : "test em2",
  "description" : "Test e2m",
  "permutations_limit" : 1,
  "metric_labels" : [ {
    "target_label" : "alias_label_name",
    "source_field" : "log_obj.string_value"
  } ],
  "metric_fields" : [ {
    "target_base_metric_name" : "alias_field_name",
    "source_field" : "log_obj.numeric_field",
    "aggregations" : [ {
      "enabled" : true,
      "agg_type" : "samples",
      "target_metric_name" : "alias_field_name_agg_func",
      "samples" : {
        "sample_type" : "max"
      }
    } ]
  } ],
  "type" : "logs2metrics",
  "logs_query" : {
    "lucene" : "logs",
    "alias" : "new_query",
    "applicationname_filters" : [ "app_name" ],
    "subsystemname_filters" : [ "sub_name" ],
    "severity_filters" : [ "unspecified", "debug", "verbose", "info", "warning", "error", "critical" ]
  }
}
```
{: codeblock}

### OutgoingWebhookPrototype
{: #cli-outgoing-webhook-prototype-example-schema}

The following example shows the format of the OutgoingWebhookPrototype object.

```json

{
  "type" : "ibm_event_notifications",
  "name" : "Event Notifications Integration",
  "url" : "https://example.com",
  "ibm_event_notifications" : {
    "event_notifications_instance_id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673",
    "region_id" : "eu-es"
  }
}
```
{: codeblock}

### PolicyPrototype
{: #cli-policy-prototype-example-schema}

The following example shows the format of the PolicyPrototype object.

```json

{
  "name" : "Med_policy",
  "description" : "Medium policy",
  "priority" : "type_high",
  "application_rule" : {
    "rule_type_id" : "is",
    "name" : "policy-test"
  },
  "subsystem_rule" : {
    "rule_type_id" : "is",
    "name" : "policy-test"
  },
  "archive_retention" : {
    "id" : "9fab83da-98cb-4f18-a7ba-b6f0435c9673"
  },
  "log_rules" : {
    "severities" : [ "unspecified", "debug", "verbose", "info", "warning", "error", "critical" ]
  }
}
```
{: codeblock}

### RulesV1CreateRuleGroupRequestCreateRuleSubgroup[]
{: #cli-rules-v1-create-rule-group-request-create-rule-subgroup-example-schema}

The following example shows the format of the RulesV1CreateRuleGroupRequestCreateRuleSubgroup[] object.

```json

[ {
  "rules" : [ {
    "name" : "mysql-parse",
    "description" : "mysql-parse",
    "source_field" : "text",
    "parameters" : {
      "parse_parameters" : {
        "destination_field" : "text",
        "rule" : "(?P<timestamp>[^,]+),(?P<hostname>[^,]+),(?P<username>[^,]+),(?P<ip>[^,]+),(?P<connectionId>[0-9]+),(?P<queryId>[0-9]+),(?P<operation>[^,]+),(?P<database>[^,]+),'?(?P<object>.*)'?,(?P<returnCode>[0-9]+)"
      }
    },
    "enabled" : true,
    "order" : 1
  } ],
  "enabled" : true,
  "order" : 1
} ]
```
{: codeblock}

### RulesV1RuleMatcher[]
{: #cli-rules-v1-rule-matcher-example-schema}

The following example shows the format of the RulesV1RuleMatcher[] object.

```json

[ {
  "subsystem_name" : {
    "value" : "mysql"
  }
} ]
```
{: codeblock}

cpe_windows_update_for_business Cookbook
========================================

Requirements
------------
* Windows 10
* Certain functionality requires release version `10.0.17134.0` or higher.

Attributes
----------
* node['cpe_windows_update_for_business']['enabled']
* node['cpe_windows_update_for_business']['branch_readiness_level']
* node['cpe_windows_update_for_business']['defer_quality_updates_period_in_days']
* node['cpe_windows_update_for_business']['defer_feature_updates_period_in_days']
* node['cpe_windows_update_for_business']['pause_quality_updates_start_time']
* node['cpe_windows_update_for_business']['pause_feature_updates_start_time']
* node['cpe_windows_update_for_business']['exclude_wu_drivers_in_quality_update']
* node['cpe_windows_update_for_business']['target_release_version']
* node['cpe_windows_update_for_business']['target_release_version_info']
* node['cpe_windows_update_for_business']['defer_quality_updates']
* node['cpe_windows_update_for_business']['defer_feature_updates']
* node['cpe_windows_update_for_business']['product_version']
* node['cpe_windows_update_for_business']['set_compliance_deadline']
* node['cpe_windows_update_for_business']['configure_deadline_for_quality_updates']
* node['cpe_windows_update_for_business']['configure_deadline_for_feature_updates']
* node['cpe_windows_update_for_business']['configure_deadline_grace_period']
* node['cpe_windows_update_for_business']['configure_deadline_grace_period_for_feature_updates']

Usage
-----
This cookbook manages the configuation of Windows Update for Business,
allowing for more granular control over update offerings and experiences
via Windows Update service.

By default, this cookbook's attributes are set to `nil` but can be
overridden by assigning values to each of the resource's properties in the API:

```
  node.default['cpe_windows_update_for_business']['enabled'] = true
  node.default['cpe_windows_update_for_business']['branch_readiness_level'] = 2
  ...
```

### `node['cpe_windows_update_for_business']['enabled']`
Manages Windows Update for Business settings when set to `true`. Otherwise, the
cookbook will not do anything.

### `node['cpe_windows_update_for_business']['branch_readiness_level']`
Controls the service channel of feature updates for a machine to receive.
Acceptable values and their corresponding service channels can be found [in the
documentation](https://docs.microsoft.com/en-us/windows/deployment/update/waas-configure-wufb#summary-mdm-and-group-policy-settings-for-windows-10-version-1703-and-later)

There are helper libraries available to set known branches in the
`CPE::WindowsUpdateForBusiness::BranchReadinessLevel` module.

### `node['cpe_windows_update_for_business']['defer_quality_updates_period_in_days']`
Defers quality updates for `n` days where `n` is a value between `0` and `35`.

### `node['cpe_windows_update_for_business']['defer_feature_updates_period_in_days']`
Defers feature updates for `n` days where `n` is a value between `0` and `365`.

### `node['cpe_windows_update_for_business']['pause_quality_updates_start_time']`
Pauses quality updates starting at a specific date, specified in `yyyy-mm-dd`
format.

### `node['cpe_windows_update_for_business']['pause_feature_updates_start_time']`
Pauses quality updates starting at a specific date, specified in `yyyy-mm-dd`
format.

### `node['cpe_windows_update_for_business']['exclude_wu_drivers_in_quality_update']`
Exclude driver updates from update searches when set to `true`.

### `node['cpe_windows_update_for_business']['target_release_version']`
Enable release targeting when set to `true`.

### `node['cpe_windows_update_for_business']['target_release_version_info']`
Beginning in Windows 10 1803 you may set a string containing a release version
that the device will try upgrade to. See the `Version` column in [the
documentation](https://aka.ms/ReleaseInformationPage) for how this value is
obtained.

### `node['cpe_windows_update_for_business']['defer_quality_updates']`
When set to `true` quality updates are deferred until the duration set in
`defer_quality_updates_period_in_days` has passed.

### `node['cpe_windows_update_for_business']['defer_feature_updates']`
When set to `true` feature updates are deferred until the duration set in
`defer_feature_updates_period_in_days` has passed.

### `node['cpe_windows_update_for_business']['product_version']`
Which major release of Windows to configure the device to pull updates for.

### `node['cpe_windows_update_for_business']['set_compliance_deadline']`
Toggles deadline compliance.

### `node['cpe_windows_update_for_business']['configure_deadline_for_quality_updates']`
Number in days allowed before enforcing quality updates.

### `node['cpe_windows_update_for_business']['configure_deadline_for_feature_updates']`
Number in days allowed before enforcing feature updates.

### `node['cpe_windows_update_for_business']['configure_deadline_grace_period']`
Number of days grace allowed before enforcing updates.

### `node['cpe_windows_update_for_business']['configure_deadline_grace_period_for_feature_updates']`
Number of days grace allowed before enforcing feature updates.

### `node['cpe_windows_update_for_business']['set_restart_warning_schedule']`
Enables or disables the option to warn users about a scheduled restart for the update
installation deadline.

### `node['cpe_windows_update_for_business']['configure_schedule_restart_warning']`
Controls how long before a scheduled restart takes place a warning will pop up.
Defaults to 4 hours, available options are 2, 4, 8, 12, 24 hours.

### `node['cpe_windows_update_for_business']['configure_schedule_imminent_restart_warning']`
Specifies the amount of time prior to a scheduled restart to display the
warning reminder to the user. Defaults to 15 minutes, 30 and 60 minutes
are the only other options.

### `node['cpe_windows_update_for_business']['set_auto_restart_required_notification_dismissal']`
Enables or disables the ability to require notifications to be dismissed
automatically or through user action

### `node['cpe_windows_update_for_business']['configure_auto_restart_required_notification_dismissal']`
Specifies how auto-restart required notifications are dismissed. 1
is automatic, 2 is user action.

### `node['cpe_windows_update_for_business']['set_elevate_non_admins']`
Controls whether non-administrative users will receive update notifications

### Example

```ruby
node.default['cpe_windows_update_for_business'].merge!({
  'branch_readiness_level' => 4,
  'defer_quality_updates_period_in_days' => 20,
  'pause_quality_updates_start_time' => '2020-04-01',
  'defer_feature_updates_period_in_days' => 250,
  'pause_feature_updates_start_time' => 1,
  'exclude_wu_drivers_in_quality_update' => true,
  'product_version' => 'Windows 10',
  'target_release_version' => true,
  'target_release_version_info' => '20H2',
})
```

Note the use of `merge!` here instead of a direct assignment. This will ensure
that the defaults are preserved. If you override the API with a direct
assignment you **must** assign every value the API supports.

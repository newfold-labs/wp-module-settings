<div style="text-align: center;">
 <a href="https://newfold.com/" target="_blank">
  <img src="https://newfold.com/content/experience-fragments/newfold/site-header/master/_jcr_content/root/header/logo.coreimg.svg/1621395071423/newfold-digital.svg" alt="Newfold Logo" title="Newfold Digital" height="42" />
 </a>
</div>

# WordPress Settings Module

This module manages the user interface for settings, determines each setting's visibility, and handles its updates.

## Module Responsibilities
- 

## Critical Paths
- 

## API

### PHP Functions

- register($name, $args)
 - $name is the internal name and will be the option name by default
 - $arguments could be:
  - Field label
  - Field description
  - Feature Name - Can be used to shortcut registering callbacks to work with the features module/API
  - Auth callback - Checks if the current user has appropriate permission, default to `manage_options`
  - Save callback - Update data at the source, default to `update_option($name)`
  - Delete callback - Handles deleting data from the source, default to `delete_option($name)`
  - Read callback - Handles fetching data from the source (e.g., database, API, etc.), default to `get_option($name)`
  - Should render callback - Checks boolean condition to see if we should show the setting, default to `__return_true`
  - Render callback — This handler handles the specific HTML that should be displayed. It defaults to rendering a basic text field (via the fields module). Would it be possible to make this easier by providing built-in methods?
  - Sanitize callback - Clean up the provided value before saving, default to `santize_text_field`
  - Validation callback - Will validate the value it valid before saving, default to `__return_true`

### REST API Endpoints

- GET newfold/settings/v1/:settingName
- POST/PATCH newfold/settings/v1/:settingName
- DELETE newfold/settings/v1/:settingName

### JavaScript API

- get($name, $default?)
- set($name, $value)
- delete($name)

## Actions & Filters

- `newfold/settings/action/onRender`
- `newfold/settings/action/onSave`
- `newfold/settings/action/onDelete`
- `newfold/settings/filter/getValue`
- `newfold/settings/filter/setValue`
- `newfold/settings/filter/shouldRender`
- `newfold/settings/filter/sanitizeValue`
- `newfold/settings/filter/isValid`
- `newfold/settings/filter/isAuthorized`

## Notes

- Settings would live in a registry and be located by name. The settings class instance would have methods that could be called.
- Settings may be stand-alone for things that need only a single value updated in the database. However, if there is advanced logic or an existing feature that should be tied to it, then the settings module should make it easy to link up to an existing feature.
- The settings module will depend on the fields module. Any fields rendered by the settings module will require that the setting has the appropriate parameters for the field.
- The fields module may be used directly to render a field, such as displaying a toggle field in the deactivation module for a given feature or setting. In such a case, you would tie a feature or setting JS API method to the field's on-change event.
- Use Alpine.js to allow field types to be usable outside of React but defined, output, and managed via PHP.
- Maybe make it easy to tie callbacks to a feature by providing a feature name
- Implement an Alpine.js toast notification that listens for events and can be loaded separately via an enqueue as needed.
- The save and delete callbacks can either return a WP_Error instance or throw an error, and this module will properly handle either case.
- Do not use the Newfold module loader. This is just a Composer package.

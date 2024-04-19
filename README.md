<div style="text-align: center;">
 <a href="https://newfold.com/" target="_blank">
  <img src="https://newfold.com/content/experience-fragments/newfold/site-header/master/_jcr_content/root/header/logo.coreimg.svg/1621395071423/newfold-digital.svg" alt="Newfold Logo" title="Newfold Digital" height="42" />
 </a>
</div>

# WordPress Settings Module

This module manages the user interface for settings, determines the visibility of each setting, and handles their updates.

## Module Responsibilities
- 

## Critical Paths
- 

## Installation

## Notes
- We may need a fields module where field types and logic can be handled separately. The settings module only needs to be able to render a field given a collection of field parameters. Fields may need to be rendered separately from the settings module.
- Do not use the Newfold module loader. This is just a Composer package.
- Consider Alpine.js to allow field types to be usable outside of React but defined, output, and managed via PHP.
- Things you register:
  - Name (this is label, but maybe can be overridden - might be default database option name)
  - Type (optional if no render callback)
    - All appropriate options for the type (e.g. placeholder text, default value, etc)
  - Callbacks (array, defined below)
  - Helper text/description
- Registering a setting requires providing the following callbacks:
  - Auth callback (optional, has default)
  - Save/Update callback
  - Delete callback
  - Read/Fetch callback
  - Should render callback
  - Render callback
    - Overrides the default
    - Should handle success, error and disabled states
    - May need toast functionality
    - Allows you to render your own field or list of sub-settings
    - May respond to Alpine data store values such as "advancedMode" for pro vs novice users
  - Sanitize callback (not required if no value is being stored, but internally should be an empty function)
  - Validation callback?
- Linking a setting to a feature should be easy (have a built-in shortcut for this)
- Settings should be auto-loaded into the data store
- If something goes wrong we should return WP_Error or throw exception
- Registering a setting requires seleting a UI type
  - Input field (email, number, etc)
  - Select field (single vs multi)
  - Toggle (should enforce booleans)
  - 

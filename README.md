# Home Assistant Automations & Blueprints

This repository contains reusable automations, scripts, and blueprints for Home Assistant. All files are organized for easy copy-paste into your own setup.

## Structure
- `automations/` — YAML files for automations
- `scripts/` — YAML files for scripts
- `blueprints/` — Blueprints for Home Assistant


## Commenting Standards
All automations should include inline comments explaining triggers, conditions, and actions. This helps with clarity, troubleshooting, and future maintenance.

## Entity Naming Conventions
Use clear, descriptive names for helpers, sensors, and automations. Example: `input_boolean.home_pressence_detected`, `timer.some_has_been_home_with_last_1_hour`.

## Troubleshooting
- YAML is indentation-sensitive. Use spaces, not tabs.
- Validate automations in Home Assistant before deploying.- Common errors: bad indentation, sequence entry misalignment, missing colons.

## References
- [Home Assistant Automations](https://www.home-assistant.io/docs/automation/)
- [Home Assistant Blueprints](https://www.home-assistant.io/docs/blueprint/)

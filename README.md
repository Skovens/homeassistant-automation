# Home Assistant Automations & Blueprints

This repository contains reusable automations, scripts, and blueprints for Home Assistant. All files are organized for easy copy-paste into your own setup.

## Structure
- `automations/` — YAML files for automations
- `scripts/` — YAML files for scripts
- `blueprints/` — Blueprints for Home Assistant


## Commenting Standards
All automations should include inline comments explaining triggers, conditions, and actions. This helps with clarity, troubleshooting, and future maintenance.

### Example: Commented Automation
```yaml
# Main presence automation: toggles helper and manages timer based on sensors, group, and manual input
alias: Home Presence
triggers:
	# Trigger: anyone arrives home
	- entity_id: group.all_persons
		trigger: state
	# Trigger: motion/contact sensors activate
	- entity_id: binary_sensor.sensor_clothes_cupboard
		from: "off"
		to: "on"
		trigger: state
	# Trigger: manual toggle of helper
	- entity_id: input_boolean.home_pressence_detected
		from: "off"
		to: "on"
		trigger: state
	# Trigger: timer expiry
	- event_type: timer.finished
		event_data:
			entity_id: timer.some_has_been_home_with_last_1_hour
		trigger: event
actions:
	# Choose block: handle presence, absence, timer expiry, and manual toggle
	- choose:
			# If anyone is home or any sensor is active, turn on helper and start timer
			- conditions:
					- condition: or
						conditions:
							- condition: state
								entity_id: group.all_persons
								state: home
							- condition: state
								entity_id: binary_sensor.sensor_clothes_cupboard
								state: "on"
				sequence:
						- target:
								entity_id: input_boolean.home_pressence_detected
							action: input_boolean.turn_on
							data: {}
						- target:
								entity_id: timer.some_has_been_home_with_last_1_hour
							action: timer.start
							data: {}
			# If timer expires, turn off helper
			- conditions:
					- condition: template
						value_template: >-
							{{ trigger.platform == 'event' and trigger.event.data.entity_id == 'timer.some_has_been_home_with_last_1_hour' }}
				sequence:
					- target:
							entity_id: input_boolean.home_pressence_detected
						action: input_boolean.turn_off
						data: {}
```

## Entity Naming Conventions
Use clear, descriptive names for helpers, sensors, and automations. Example: `input_boolean.home_pressence_detected`, `timer.some_has_been_home_with_last_1_hour`.

## Troubleshooting
- YAML is indentation-sensitive. Use spaces, not tabs.
- Validate automations in Home Assistant before deploying.- Common errors: bad indentation, sequence entry misalignment, missing colons.

## References
- [Home Assistant Automations](https://www.home-assistant.io/docs/automation/)
- [Home Assistant Blueprints](https://www.home-assistant.io/docs/blueprint/)

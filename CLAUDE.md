# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Home Assistant custom integration for Daikin devices using the Daikin Onecta API. The integration allows users to control their Daikin HVAC systems through Home Assistant.

## Development Commands

### Testing
```bash
pytest                    # Run all tests
pytest tests/test_init.py # Run specific test file
```

### Linting and Formatting
```bash
pre-commit run --all-files  # Run all pre-commit hooks
ruff check .                # Check code with ruff
ruff format .               # Format code with ruff
flake8                      # Run flake8 linting
```

### Pre-commit Setup
```bash
pre-commit install          # Install pre-commit hooks
```

## Code Architecture

### Core Components
- `__init__.py` - Main integration setup and entry point
- `config_flow.py` - OAuth2 configuration flow for Daikin API authentication
- `coordinator.py` - Data update coordinator for managing API polling
- `daikin_api.py` - API client for communicating with Daikin Onecta cloud service

### Platform Components
The integration provides multiple Home Assistant platform types:
- `climate.py` - HVAC climate control entities
- `sensor.py` - Temperature, humidity, and status sensors
- `water_heater.py` - Water heater control entities
- `switch.py` - On/off switches for various functions
- `select.py` - Selection entities for modes and settings
- `binary_sensor.py` - Binary status sensors
- `button.py` - Button entities for actions

### Key Architecture Patterns
- Uses Home Assistant's OAuth2 flow for authentication with Daikin Developer Portal
- Implements coordinator pattern for efficient data polling and caching
- Each platform registers entities based on available device capabilities
- Follows Home Assistant entity and device registry patterns

### Configuration
- Integration uses `manifest.json` for Home Assistant integration metadata
- Authentication requires OAuth2 credentials from Daikin Developer Portal
- Supports configurable polling intervals and update frequency settings

### Testing Structure
- Tests located in `tests/` directory
- Uses pytest with Home Assistant test fixtures
- Includes configuration flow tests, coordinator tests, and initialization tests
- Test coverage configured in `setup.cfg`

## Development Notes

### Code Style
- Line length: 150 characters (ruff) / 88 characters (flake8/isort)
- Uses ruff for linting and formatting
- Import sorting handled by reorder-python-imports
- Pre-commit hooks enforce code quality

### OAuth2 Integration
- Requires Daikin Developer Portal account and application setup
- Uses Home Assistant's built-in OAuth2 helper
- Redirect URI typically `https://my.home-assistant.io/redirect/oauth`

### Device Discovery
- Devices automatically discovered after OAuth2 authentication
- Each device type creates appropriate platform entities
- Device capabilities determine which platforms are available
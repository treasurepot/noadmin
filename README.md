# NoAdmin - System Management AI Assistant

## Overview

NoAdmin is a command-line AI assistant designed to help users execute system management tasks through natural language queries. It leverages Large Language Models (LLMs) to interpret user questions and generate appropriate terminal commands, with built-in verification and safety features. The tool supports multiple LLM providers, internationalization, and customizable system roles.

**Version**: v0.0.3  
**License**: Not specified (assume open source)

## Architecture

NoAdmin follows a modular architecture with these key components:

1. **Core Script (`noadmin.sh`)**: Main executable that handles user interaction, API communication, and command execution
2. **Internationalization System**: Language resource files for English and Chinese interfaces
3. **Configuration Management**: JSON-based configuration file for storing provider settings and preferences
4. **Provider Abstraction Layer**: Supports multiple LLM providers (DeepSeek, OpenAI, Z.ai, custom)
5. **Command Verification System**: AI-powered command explanation and safety verification

## Prerequisites

### System Requirements
- **Operating System**: Linux, macOS, or Unix-like systems with bash shell
- **Shell**: Bash 4.0 or higher
- **Dependencies**:
  - `curl` for API communication
  - `jq` or `python3` for JSON parsing (recommended)
  - `unzip` for deployment (if using store.zip)

### API Requirements
- API key from at least one supported LLM provider:
  - DeepSeek (default)
  - OpenAI
  - Z.ai
  - Custom providers

## Quick Start

1. **Deploy the project**:
   ```bash
   bash 1click_deploy.sh [optional_target_directory]
   ```

2. **Navigate to the deployment directory**:
   ```bash
   cd packed_project  # or your specified directory
   ```

3. **Install NoAdmin**:
   ```bash
   sudo cp -r usr/local/share/noadmin_v0.0.3 /usr/local/share/
   sudo cp home/admin/noadmin/noadmin.sh /usr/local/bin/?
   sudo chmod +x /usr/local/bin/?
   ```

4. **Configure your LLM provider**:
   ```bash
   ? --config
   ```

5. **Start using NoAdmin**:
   ```bash
   ? "how to check disk space"
   ```

## Deployment Guide

### Automated Deployment
The provided script automates deployment with these steps:

1. **Create deployment directory**: Creates `packed_project` by default
2. **Restore project structure**: Recreates the directory hierarchy from embedded JSON
3. **Extract language files**: Installs English and Chinese localization files
4. **Install main script**: Places `noadmin.sh` in the appropriate location
5. **Extract additional files**: Unzips `store.zip` if present (for binary/excluded files)
6. **Clean up**: Removes temporary structure files

### Manual Deployment
If you need to deploy manually:

1. Create the directory structure:
   ```bash
   sudo mkdir -p /usr/local/share/noadmin_v0.0.3/locales
   ```

2. Copy language files:
   ```bash
   sudo cp usr/local/share/noadmin_v0.0.3/locales/*.sh /usr/local/share/noadmin_v0.0.3/locales/
   ```

3. Install the main script:
   ```bash
   sudo cp home/admin/noadmin/noadmin.sh /usr/local/bin/?
   sudo chmod +x /usr/local/bin/?
   ```

### Post-Deployment
After deployment, the script will be accessible as `?` from any terminal location.

## Configuration

### Initial Setup
Run the configuration wizard:
```bash
? --config
```

### Configuration Options
1. **Provider Selection**:
   - DeepSeek (default)
   - OpenAI
   - Z.ai
   - Custom providers

2. **System Role Configuration**:
   - Default system role (auto-detects OS)
   - Custom system role

3. **Language Settings**:
   - English (default)
   - Chinese

### Configuration File
Location: `~/.noadmin_config`

Format:
```
DEFAULT_PROVIDER=deepseek
SYSTEM_ROLE=<system role text>
UI_LANGUAGE=en
deepseek=https://api.deepseek.com/v1/chat/completions|API_KEY|deepseek-chat|Bearer|deepseek
```

## Usage

### Basic Usage
```bash
? "your question here"
```

### Examples
```bash
? "how to check disk space"
? "list running processes"
? "install nginx web server"
? "configure firewall for port 80"
```

### Command Options
- `? --config`: Configure LLM providers and settings
- `? --change`: Change default LLM provider
- `? --lang`: Change interface language (en/zh)
- `? --reset`: Clear all configurations
- `? --help`: Show help message

### Interactive Features
1. **Command Verification**: Type `v` when prompted to verify a command before execution
2. **Confirmation Prompt**: Always confirms before executing commands (y/N/v)
3. **Language Detection**: Automatically detects question language for appropriate responses

## File Structure

```
packed_project/
├── usr/
│   └── local/
│       └── share/
│           └── noadmin_v0.0.3/
│               └── locales/
│                   ├── en.sh          # English language resources
│                   └── zh.sh          # Chinese language resources
├── home/
│   └── admin/
│       └── noadmin/
│           └── noadmin.sh            # Main executable script
└── store.zip                         # Optional binary/excluded files
```

### Key Files Description
1. **noadmin.sh**: Main script with all functionality
2. **en.sh/zh.sh**: Internationalization files containing UI strings
3. **structure.json**: Deployment manifest (temporary, removed after deployment)
4. **store.zip**: Optional archive for additional files

## Troubleshooting

### Common Issues

1. **"Command not found: ?"**
   - Ensure the script is installed to `/usr/local/bin/?`
   - Check file permissions: `sudo chmod +x /usr/local/bin/?`

2. **API Connection Errors**
   - Verify your API key is correct
   - Check internet connectivity
   - Ensure the provider endpoint is accessible

3. **JSON Parsing Errors**
   - Install `jq`: `sudo apt-get install jq` (Debian/Ubuntu)
   - Or ensure Python 3 is available

4. **Permission Denied Errors**
   - Some commands require `sudo` - the AI should add this automatically
   - If not, you can manually add `sudo` before executing

5. **Language File Issues**
   - Default fallback to English if language files are missing
   - Check file permissions in `/usr/local/share/noadmin_v0.0.3/locales/`

### Debug Mode
For advanced debugging, you can:
1. Check the configuration file: `cat ~/.noadmin_config`
2. Test API connectivity manually with curl
3. Examine temporary debug files in `/tmp/noadmin_*`

### Logs
- Configuration: `~/.noadmin_config`
- API responses: `/tmp/noadmin_verify_debug.log` (temporary)

## Contributing

### Development
1. Fork the repository
2. Create a feature branch
3. Make changes with clear commit messages
4. Test thoroughly
5. Submit a pull request

### Adding New Features
1. **New LLM Providers**: Add provider configuration in `init_config()` function
2. **New Languages**: Create language file in `locales/` directory
3. **Enhanced Verification**: Extend `verify_command()` function

### Testing
- Test with various system management queries
- Verify command safety features
- Test internationalization support
- Ensure backward compatibility

### Code Style
- Follow existing bash scripting conventions
- Add comments for complex logic
- Maintain internationalization support
- Include error handling for all operations

### Security Considerations
- Never commit API keys or sensitive data
- Validate all user inputs
- Sanitize commands before execution
- Maintain the verification system for safety

---

**Note**: This tool executes system commands automatically. Always verify commands (use 'v' option) before execution, especially for operations that modify system files or configurations. The developers are not responsible for any system damage caused by improper use.

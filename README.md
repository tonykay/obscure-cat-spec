# ocat - Obscure Cat Utility

A bash utility that safely displays files containing export statements with sensitive data obscured.

## Overview

`ocat` reads files containing environment variable exports and obscures sensitive values while preserving the file structure. It's designed to help you safely view configuration files without exposing secrets.

## Features

- Obscures sensitive data in export statements
- Shows first 4 characters of values 8+ characters long
- Completely obscures values less than 8 characters
- Handles different quoting styles (none, single quotes, double quotes)
- Preserves comments and commented export lines
- Never modifies the original file
- Outputs to STDOUT for safe viewing

## Usage

```bash
# Show help
./ocat -h
./ocat --help

# Use default file (~/secrets/secret-env-vars.env)
./ocat

# Specify a custom file
./ocat /path/to/your/exports.env
./ocat my-secrets.env
```

## Examples

### Input file content:
```bash
export LLAMA_API_KEY=993
export AURA_INSTANCEID=6fc2
export AURA_INSTANCENAME=Insta1
export AAP2_PASSWORD="9b5bb6cfd"
export SHORT_KEY=abc123
# export OLD_SECRET=supersecret123
```

### Output:
```bash
export LLAMA_API_KEY=993<OBSCURED>
export AURA_INSTANCEID=6fc2<OBSCURED>
export AURA_INSTANCENAME=Inst<OBSCURED>
export AAP2_PASSWORD="9b5b<OBSCURED>"
export SHORT_KEY=<OBSCURED>
# export OLD_SECRET=supe<OBSCURED>
```

## Supported Export Formats

- `export VAR=value`
- `export VAR="value"`
- `export VAR='value'`
- `# export VAR=value` (commented exports)

## Installation

1. Make the script executable:
   ```bash
   chmod +x ocat
   ```

2. Optionally, move to a directory in your PATH:
   ```bash
   sudo mv ocat /usr/local/bin/
   ```

## Configuration

The obscuring string `<OBSCURED>` is stored as an environment variable `OBSCURE_STRING` and can be customized if needed.

## Security Note

This utility is designed for safe viewing of configuration files. It never modifies the original files and only outputs obscured content to STDOUT.
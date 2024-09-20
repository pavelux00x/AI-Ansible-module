# Ansible Azure OpenAI Module

This Ansible module allows users to generate Linux commands based on task descriptions via an API call to Azure OpenAI. It's designed to assist in automating tasks through Ansible, where simple descriptions of tasks can be translated into executable Linux commands.

## Overview

The module interacts with Azure OpenAI's API by sending a prompt that describes a task (such as "create a directory called test"). The response from the API will be the corresponding Linux command (e.g., `mkdir test`), which can then be used in automation scripts.

## Features

- **Dynamic Command Generation**: Provide a task description and get back a usable Linux command.
- **Flexible**: Works with various automation scenarios within Ansible.
- **Simple Input/Output**: The module focuses on minimalistic prompts and clear, actionable responses.

## Requirements

- Python 3.x
- Ansible 2.4+
- `requests` Python library (you can install it with `pip install requests`)
- Azure OpenAI API access

## Installation

1. Copy the Python file into your Ansible module directory (e.g., `library/` folder in your playbook).
2. Ensure the necessary dependencies are installed:
   ```bash
   pip install requests
   ```

## Usage

Here is an example of how to use the module within an Ansible playbook.

### Example Playbook

```yaml
---
- hosts: localhost
  tasks:
    - name: Generate a command for directory creation
      azure_openai:
        api_key: "{{ api_key }}"
        message: "Create a directory called test"
      register: result

    - name: Display the generated command
      debug:
        var: result.message
```

In this playbook:
- **api_key**: The API key required to access the Azure OpenAI service.
- **message**: A description of the task you want to automate (e.g., creating a directory).

### Example Output

```yaml
TASK [Display the generated command] *******************************************
ok: [localhost] => {
    "result.message": "mkdir test"
}
```

## Options

| Parameter | Required | Description                                                                 |
|-----------|----------|-----------------------------------------------------------------------------|
| api_key   | Yes      | Your API key to access Azure OpenAI.                                         |
| message   | Yes      | A task description to be sent to Azure OpenAI for generating a Linux command.|

## Return Values

| Name            | Type   | Description                                                                 |
|-----------------|--------|-----------------------------------------------------------------------------|
| original_message| string | The original task description passed to the module.                         |
| response_message| string | The generated Linux command that corresponds to the task description.       |

## Error Handling

If the module encounters an error when calling the API (e.g., network issues or an invalid API key), it will return an error message explaining what went wrong.

## License

GNU General Public License v3.0+ (see COPYING or https://www.gnu.org/licenses/gpl-3.0.txt)

## Author

- **Pavel** (@levap00x)

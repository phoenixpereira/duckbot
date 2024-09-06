## Internal Code Documentation: HiGroup Class

### Table of Contents

* [1. Introduction](#1-introduction)
* [2. Class Definition: HiGroup](#2-class-definition-higroup)
    * [2.1. Constructor](#21-constructor)
    * [2.2. `me` Command](#22-me-command)
    * [2.3. `there` Command](#23-there-command)
* [3. Usage](#3-usage)

### 1. Introduction

This code defines a `HiGroup` class that provides a set of commands for greeting users. The `HiGroup` class is designed to be used with the Discord.py library's `app_commands` framework.

### 2. Class Definition: HiGroup

The `HiGroup` class defines two commands: `me` and `there`. Both commands are subcommands of the `hi` group, which provides a logical grouping for these greeting commands.

#### 2.1. Constructor

The `__init__` method initializes the `HiGroup` object with a name and description.

| Parameter | Type | Description |
|---|---|---|
| `name` | str | The name of the group, used in the slash command path. |
| `description` | str | A brief description of the group's purpose. |

**Code Example:**

```python
def __init__(self):
    super().__init__(name="hi", description="Commands to greet users")
```

#### 2.2. `me` Command

The `me` command greets the user who invoked the command.

| Parameter | Type | Description |
|---|---|---|
| `interaction` | Interaction | The interaction object representing the command invocation. |

**Code Example:**

```python
@app_commands.command(name="me", description="Say hi to you.")
async def me(self, interaction: Interaction):
    user = interaction.user
    await interaction.response.send_message(f"Hi {user.mention}!")
```

**Explanation:**

1. The `@app_commands.command` decorator defines the command name, description, and its function.
2. The `interaction` parameter provides information about the command invocation, including the user who initiated it.
3. The code retrieves the user who invoked the command using `interaction.user`.
4. The code sends a message back to the user using `interaction.response.send_message`, mentioning the user in the message.

#### 2.3. `there` Command

The `there` command sends a generic greeting message.

| Parameter | Type | Description |
|---|---|---|
| `interaction` | Interaction | The interaction object representing the command invocation. |

**Code Example:**

```python
@app_commands.command(name="there", description="Say hi.")
async def there(self, interaction: Interaction):
    await interaction.response.send_message("Hi there!")
```

**Explanation:**

1. The `@app_commands.command` decorator defines the command name, description, and its function.
2. The code sends a simple greeting message using `interaction.response.send_message`.

### 3. Usage

To use the `HiGroup` class, you need to register it with a Discord.py bot instance using the `add_app_command` method. Once registered, users can invoke the commands by typing `/hi me` or `/hi there` in a Discord channel.

**Code Example:**

```python
bot = commands.Bot(...)
bot.add_app_command(hi_group)
```

**Example Usage:**

* **User:** `/hi me`
* **Bot:** Hi @user!
* **User:** `/hi there`
* **Bot:** Hi there! 

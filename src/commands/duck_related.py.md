## Duck Commands Documentation 🦆

### Table of Contents

| Section | Description |
|---|---|
| **Overview** | A brief description of the DuckCommands class and its purpose. |
| **Class Structure** | Detailed explanation of the DuckCommands class, its methods, and attributes. |
| **API Usage** |  Details on how to use the commands within a Discord bot. |
| **Data Sources** | Information on the data sources used for facts and jokes. |

### Overview

The `DuckCommands` class provides a collection of fun duck-related commands for a Discord bot. It leverages the `app_commands` framework from the Discord.py library to define commands that users can interact with. These commands include:

* **`duck gif`**:  Sends a random duck GIF.
* **`duck pic`**: Sends a random duck picture.
* **`duck fact`**: Sends a random duck fact.
* **`duck joke`**: Tells a random duck-related joke.

### Class Structure 

**`DuckCommands` Class:**

```python
class DuckCommands(app_commands.Group):
    def __init__(self):
        super().__init__(name="duck", description="Fun duck-related commands")

    # ... methods ...
```

This class inherits from `app_commands.Group`, which allows it to be registered as a command group within a Discord bot.

**Methods:**

* **`get_duck_image()`**:
    * This method fetches a random duck image from the `random-d.uk` API.
    * It utilizes `aiohttp` for asynchronous HTTP requests.
    * The API endpoint `https://random-d.uk/api/v2/random?type=jpg` is used to retrieve a random duck image in JPEG format.
    * The method handles potential errors during image fetching and returns the image URL if successful, otherwise returns `None`.

* **`duck_gif(interaction: Interaction)`**:
    * This command uses the `get_tenor_gif` function from the `utils.tenor` module to retrieve a random duck GIF from Tenor.
    * If a GIF is found, an embed message is created displaying the GIF and sent to the channel.
    * If no GIF is found, an error message is sent to the channel.

* **`duck_pic(interaction: Interaction)`**:
    * This command calls the `get_duck_image()` method to fetch a random duck picture.
    * If successful, an embed message containing the picture is sent to the channel.
    * If no picture is found, an error message is sent to the channel.

* **`duck_fact(interaction: Interaction)`**:
    * This command randomly selects a duck fact from the `DUCK_FACTS` list and sends it as a message to the channel.

* **`duck_joke(interaction: Interaction)`**:
    * This command randomly selects a duck joke from the `DUCK_JOKES` list and sends it as a message to the channel.

### API Usage

The `DuckCommands` class is intended to be used within a Discord bot. To use it:

1. **Import the class:**
   ```python
   from your_module import DuckCommands
   ```

2. **Instantiate the class:**
   ```python
   duck_commands = DuckCommands()
   ```

3. **Register the command group with your bot:**
   ```python
   bot.add_app_command(duck_commands)
   ```

Once registered, users can access the duck-related commands by typing `/duck` followed by the desired command (e.g., `/duck gif`, `/duck fact`).

### Data Sources

The duck facts and jokes are stored in the `DUCK_FACTS` and `DUCK_JOKES` lists respectively. These lists are defined in the `constants.duck_data` module. You can customize these lists by adding or removing facts and jokes as needed.

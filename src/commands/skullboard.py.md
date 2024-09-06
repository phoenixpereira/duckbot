## 🤖 Skullboard Manager Documentation

### Table of Contents

| Section | Description |
|---|---|
| [1. Overview](#1-overview) | General description of the code's functionality. |
| [2. Class Structure](#2-class-structure) | Detailed explanation of each class and its methods. |
|   [2.1. SkullboardManager](#21-skullboardmanager) | Manages Discord activities related to the skullboard. |
|   [2.2. Response](#22-response) | A class defining the return type for command functions. |
|   [2.3. SkullGroup](#23-skullgroup) | A group of Slash commands related to skullboard queries. |
| [3. Helper Functions](#3-helper-functions) | Explanation of helper functions used throughout the code. |
| [4. Data Structures](#4-data-structures) | Description of data structures used in the code. |
| [5. Constants](#5-constants) | Definition of constants used in the code. |

### 1. Overview

This code defines a set of classes and functions for managing the Skullboard, a feature within a Discord server for tracking popular posts and active users. The core functionality revolves around a `SkullboardManager` class, responsible for handling reactions and updating or sending skullboard messages. The code also includes a `SkullGroup` class that defines a collection of Slash commands related to skullboard queries, providing users with access to information such as user rankings, Hall of Fame, weekly top posts, statistical distributions, and user-specific skullboard stats.

### 2. Class Structure

#### 2.1. SkullboardManager

The `SkullboardManager` class is responsible for handling Discord activities related to the skullboard. It leverages the `SkullboardDB` class to interact with the database, storing and retrieving data related to skullboard posts and user statistics. 

| Method | Description |
|---|---|
| `__init__(self, client: Client)` | Initializes the `SkullboardManager` instance, setting up the client connection and database connection. |
| `get_reaction_count(self, message, emoji)` | Returns the count of a specific emoji reaction on a given message. |
| `handle_skullboard(self, message, skullboard_channel_id)` | Handles reactions to messages, updating or creating skullboard messages as needed. |
| `update_or_send_skullboard_message(self, channel, message, current_count, emoji)` | Updates an existing skullboard message or sends a new one based on the current reaction count. |
| `get_gif_url(view_url)` | Extracts the GIF URL from a Tenor view URL. |
| `edit_or_send_skullboard_message(self, channel, message, current_count, emoji, send=False, skullboard_message_id=None)` | Edits an existing skullboard message or sends a new one, including appropriate content and embeds. |

#### 2.2. Response

The `Response` class defines the return type for command functions within the `SkullGroup`. It encapsulates various potential responses, including an optional embed, image, and plain text message.

| Attribute | Description |
|---|---|
| `embed (Embed)` | Optional `Embed` object for rich content in the response. |
| `img (BytesIO)` | Optional `BytesIO` object for image attachments in the response. |
| `message (str)` | Optional string for plain text message content. |

#### 2.3. SkullGroup

The `SkullGroup` class defines a group of Slash commands related to skullboard queries. It utilizes a wrapper function (`interaction_handler`) to handle interactions and potential errors, providing a consistent response mechanism for all commands.

| Command | Description |
|---|---|
| `/skull about` | Provides information about the Skullboard and its functionalities. |
| `/skull rank` | Displays the top skullboard users of all time. |
| `/skull hof` | Displays the top skullboard posts of all time. |
| `/skull week` | Displays the top skullboard posts from the current week. |
| `/skull stats` | Displays the distribution of skullboard posts over various timeframes (week, month, year, all-time). |
| `/skull user` | Displays skullboard stats for a specific user, including post count and percentile ranking. |

### 3. Helper Functions

The code includes several helper functions that are used throughout the code for various tasks.

| Function | Description |
|---|---|
| `time.get_day_from_timestamp(timestamp)` | Extracts the day from a given timestamp. |
| `utils.plotting.get_histogram_image(data, xlabel, ylabel, title, vline=None)` | Generates a histogram image from provided data. |

### 4. Data Structures

The code utilizes the following data structures:

| Structure | Description |
|---|---|
| `collections.Counter` | Used to count the frequency of elements in a list. |

### 5. Constants

The code utilizes the following constants:

| Constant | Description |
|---|---|
| `LIGHT_GREY` | A constant representing a light grey color used for embeds. |
| `SKULLBOARD_CHANNEL_ID` | An environment variable storing the channel ID for the Skullboard. |

# FAQ Bot Documentation

## Table of Contents
- [FAQGroup Class](#faqgroup-class)
    - [rsp Command](#rsp-command)
    - [cpc Command](#cpc-command)
- [FNGGroup Class](#fnggroup-class)
    - [about Command](#about-command)
    - [food Command](#food-command)


## FAQGroup Class
The `FAQGroup` class defines a group of commands related to frequently asked questions. It is a `discord.app_commands.Group` object and has the following attributes and methods:

| Attribute | Description |
|---|---|
| `name` |  The name of the group, which is "faq". |
| `description` | A brief description of the group, which is "Answers to common questions". |
| `add_command(FNGGroup())` | Adds the `FNGGroup` class as a subcommand to the `FAQGroup` class. |

### rsp Command
The `rsp` command provides information about the "Ravi's Study Program" (RSP).

```python
@app_commands.command(name="rsp", description="Learn about RSP")
async def rsp(self, interaction: Interaction):
    rsp_info = (
        "Participating in RSP (Ravi's Study Program) could possibly be the single most beneficial thing you can do while you're at University to land a job as a Software Engineer at a great company.\n\n"
        "The program is run by current and former students and tutors from The University of Adelaide, and provides students with the exact steps they need to take to prepare themselves to pass interviews at big tech/FAANG companies. There are very impressive numbers of people that land internships at these companies after successfully completing the program.\n\n"
        "RSP is an intensive programming bootcamp run each summer break. If you wish to get involved, keep an eye out for flyers on campus towards the end of Semester 2, as well as advertisements that are posted in various computer science related discord servers.\n"
    )
    await interaction.response.send_message(rsp_info)
```

This method:
- Defines a command named "rsp" with a description "Learn about RSP".
- When invoked, it sends a message to the user containing information about RSP.

### cpc Command
The `cpc` command provides information about the "Competitive Programming Club" (CPC).

```python
@app_commands.command(name="cpc", description="Learn about CPC")
async def cpc(self, interaction: Interaction):
    cpc_info = (
        "The Competitive Programming Club (CPC) is the University of Adelaide's home for competitive programming. Whether you're just getting started, or looking to flex those programming muscles, the CPC offers a wide range of events and opportunities for those interested.\n\n"
        "There's no cost for registration and you can find out more here:\n"
        "https://acpc.io/\n"
    )
    await interaction.response.send_message(cpc_info)
```

This method:
- Defines a command named "cpc" with a description "Learn about CPC".
- When invoked, it sends a message to the user containing information about CPC, including a link to the CPC website.

## FNGGroup Class
The `FNGGroup` class defines a group of commands related to "Friday Night Games" (FNG). It is a `discord.app_commands.Group` object and has the following attributes and methods:

| Attribute | Description |
|---|---|
| `name` |  The name of the group, which is "fng". |
| `description` | A brief description of the group, which is "Learn about FNG". |

### about Command
The `about` command provides information about FNG.

```python
@app_commands.command(
    name="about", description="Provides information about Friday Night Games (FNG)"
)
async def about(self, interaction: Interaction):
    fng_info = (
        "Friday Night Games (FNG) is a regular Computer Science Club event where the Duck Lounge (Located in EM110) hosts a weekly games night from 5PM where members commonly play amongst a Nintendo Switch and board games.\n"
        "Moreover, on the final Friday of each month within semester, we have free food for all members! Type ``/faq fng food`` to find out when the next FNG with food will be.\n\n"
        "Join us for games and fun!\n"
    )
    await interaction.response.send_message(fng_info)
```

This method:
- Defines a command named "about" with a description "Provides information about Friday Night Games (FNG)".
- When invoked, it sends a message to the user containing information about FNG.

### food Command
The `food` command outputs the date of the next Friday Night Games with free food.

```python
@app_commands.command(
    name="food",
    description="Outputs the date of the next Friday Night Games with food",
)
async def food(self, interaction: Interaction):
    # Manually inputting dates
    date_stack = [
        dt.datetime(2024, 10, 25, 17),
        dt.datetime(2024, 8, 30, 17),
        dt.datetime(2024, 7, 26, 17),
        dt.datetime(2024, 5, 31, 17),
        dt.datetime(2024, 4, 26, 17),
        dt.datetime(2024, 3, 29, 17),
    ]

    # Checking if the tail date has already passed
    curr_date = dt.datetime.now()
    if curr_date > date_stack[-1]:
        while (
            len(date_stack) > 0 and curr_date > date_stack[-1]
        ):  # length check was added to prevent access of first element when list was empty - this would cause a compiler error
            date_stack.pop()

    # Printing next time for Games Night
    if len(date_stack) == 0:
        await interaction.response.send_message(
            "The next Friday Night Games with food will be next year. Thank you for being a valued member!"
        )
        return

    # Determining if games night is on the same day as day of function call
    time_difference = date_stack[-1].date() - curr_date.date()
    if time_difference.days <= 1:
        time_difference_hours = round(time_difference.seconds / 3600, 2)
        if time_difference_hours < 1:
            await interaction.response.send_message(
                f"The next Friday Night Games with food is on today in {time_difference_hours} hour at 5pm. Join us in the Duck Lounge!"
            )
        else:
            await interaction.response.send_message(
                f"The next Friday Night Games with food is on today in {time_difference_hours} hours at 5pm. Join us in the Duck Lounge!"
            )
        return

    # Determining if games night is on the next day of function call
    if time_difference.days < 2 and time_difference.days > 1:
        await interaction.response.send_message(
            f"The next Friday Night Games with food is on tomorrow. Join us in the Duck Lounge at 5pm!"
        )
        return

    # Determining whether date needs a st, nd, rd or rth
    date_num = date_stack[-1].strftime("%d")
    date_day = date_stack[-1].strftime("%B")
    if date_num in {1, 21, 31}:  # st
        await interaction.response.send_message(
            f"The next Friday Night Games with food will be held in {time_difference.days} days on the {date_num}st of {date_day}"
        )
    elif date_num in {2, 22}:  # nd
        await interaction.response.send_message(
            f"The next Friday Night Games with food will be held in {time_difference.days} days on the {date_num}nd of {date_day}"
        )
    elif date_num in {3, 23}:  # rd
        await interaction.response.send_message(
            f"The next Friday Night Games with food will be held in {time_difference.days} days on the {date_num}rd of {date_day}"
        )
    else:  # th
        await interaction.response.send_message(
            f"The next Friday Night Games with food will be held in {time_difference.days} days on the {date_num}th of {date_day}"
        )
```

This method:
- Defines a command named "food" with a description "Outputs the date of the next Friday Night Games with food".
- Contains a list of dates (`date_stack`) for FNG with food.
- Calculates the time difference between the current date and the next FNG with food.
- Sends a message to the user containing the date of the next FNG with food, based on the calculated time difference.

**Key Points:**
- The `food` command uses a manual list of dates for FNG with food. This could be improved by using a more dynamic method for retrieving these dates, such as reading them from a file or database.
- The command provides different messages depending on the time difference between the current date and the next FNG with food. This enhances user experience by providing more specific information.

**Potential Improvements:**
- Dynamically retrieving FNG with food dates to avoid manual updates.
- Implementing a calendar integration for displaying upcoming FNG dates.
- Adding a feature to allow users to set reminders for upcoming FNG events. 

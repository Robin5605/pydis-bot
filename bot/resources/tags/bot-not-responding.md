---
embed:
    title: "Bot not responding to commands?"
---

```py
@bot.event
async def on_message(message):
  ...
```
If your code looks like this - it could be the reason why your bot isn't responding to commands.
Using the `@bot.event` decorator together with `async def on_message(...)` is problematic because it overrides the default command handler.

There are two solutions:
1. Use a listener rather than an event (recommended):
```py
@bot.listen()
async def on_message(message):
  ...
```

2. Or [`process_commands`](https://discordpy.readthedocs.io/en/stable/ext/commands/api.html?highlight=process_commands#discord.ext.commands.Bot.process_commands):
```py
@bot.event
async def on_message(message):
  ...
  await bot.process_commands(message)
```

It is important that you only pick one or the other. Using both would make the bot respond twice to all commands.

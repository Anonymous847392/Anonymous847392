# Roblox Bot Commands Documentation

## Overview

This bot script allows players to control actions in the game through chat commands prefixed with "-". It responds to various commands to perform actions like emotes, movements, and providing information.

## Commands

### Basic Commands

- `-hello`
  - Greets the player with a friendly message.

- `-dance`
  - Makes the player's character perform a dance animation.

- `-jump`
  - Makes the player's character jump once.

- `-wave`
  - Makes the player's character wave.

### Utility Commands

- `-help`
  - Displays a list of available commands and their descriptions.

### Command Usage

- To use a command, type it in the chat preceded by a "-" (e.g., `-hello`, `-dance`).

- Commands are not case-sensitive (`-Hello` and `-hello` will produce the same result).

### Examples

1. Typing `-hello` in the chat will trigger the bot to respond with a greeting message.

2. Typing `-dance` will trigger the bot to make the player's character perform a dance animation.

3. Typing `-help` will display a message listing all available commands.

### Error Handling

- If an unrecognized command is typed, the bot will respond with a message indicating that the command is unknown. It will also prompt the player to type `-help` for a list of valid commands.

## Implementation

### Script Setup

1. Insert the following Lua script into a `Script` object in `ServerScriptService` or `StarterPlayerScripts` in Roblox Studio.

```lua
-- Simple Roblox Bot Script

-- Function to send chat messages
local function sendChatMessage(message)
    game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(message, "All")
end

-- Function to handle chat commands
local function handleChatCommand(command)
    if command:lower() == "hello" then
        sendChatMessage("Hello, I am your friendly bot!")
    elseif command:lower() == "dance" then
        sendChatMessage("/e dance")
    elseif command:lower() == "jump" then
        sendChatMessage("/e jump")
    elseif command:lower() == "wave" then
        sendChatMessage("/e wave")
    elseif command:lower() == "help" then
        sendChatMessage("Available commands: hello, dance, jump, wave")
    else
        sendChatMessage("Unknown command. Type 'help' for a list of commands.")
    end
end

-- Listen for chat messages
game:GetService("Players").LocalPlayer.Chatted:Connect(function(message)
    if message:sub(1, 1) == "-" then
        local command = message:sub(2):lower() -- Remove the "-" prefix and convert to lowercase
        handleChatCommand(command)
    end
end)

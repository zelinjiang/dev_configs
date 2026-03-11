# iTerm2 Settings

Settings -> Profiles

- Text: 
  - Font: Source Code Pro
  - Font Size 12
  - Uncheck "Blink Cursor"
- Colors
  - Cursor: c7c7c7
  - Cursor Boost 0%

# Starship

Put the starship.toml file under ~/.config/starship.toml

Starship formats the current command prompt, not the history. 

# Settings in .zshrc 

Commands in zshrc are for formating past commands.

Add below lines into the bottom of the.zshrc file. 

``````zsh
## iTerm2 settings
eval "$(starship init zsh)"  # Starship settings in ~/.config/starship.toml
# Color the history command for easier sectioning and avoid extra blank lines
typeset -g __pretty_history_cmd=
CLEAR_LINE=$'\033[2K'
CMD_COLOR=$'\033[1;32m'     # Bright green; Bright magenta = "\033[1;35m"
CMD_SYMBOL='➜ '             # Other choices: "$", "❯", "➜", "›"
RESET_COLOR=$'\033[0m'
_caccept() {
  emulate -L zsh
  __pretty_history_cmd=$BUFFER
  zle auto-suffix-retain 2>/dev/null
  builtin printf '\r%s\r' "$CLEAR_LINE"
  zle .accept-line
}
zle -N accept-line _caccept
preexec() {
  emulate -L zsh
  builtin printf '\033[A\r%s%s%s%s%s\n' \
    "$CLEAR_LINE" "$CMD_COLOR" "$CMD_SYMBOL" "$__pretty_history_cmd" "$RESET_COLOR"
  __pretty_history_cmd=
}
``````


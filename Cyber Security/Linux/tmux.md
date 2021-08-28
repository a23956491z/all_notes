## Hotkey
### Session
session with name
```bash
$ tmux new -s SESSION_NAME
```

### Copy & paste
`Ctrl+B [` Selection mode
Selection mode:
* `Ctrl+Space` Start select
* `Ctrl+w` copy
* `q` quit

`Ctrl+B ]` Paste

### Split
`Ctrl+B %` vertically split

## Tmux plugin manager
```bash
$ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

`~/.tmux.conf`

```
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'github_username/plugin_name#branch'
# set -g @plugin 'git@github.com:user/plugin'
# set -g @plugin 'git@bitbucket.com:user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

reload tmux
```bash
# type this in terminal if tmux is already running
$ tmux source ~/.tmux.conf
```

### Install
1. add new plugin to `~/.tmux.conf` with `set -g @plugin '...'`
2. Press prefix + I (capital i) to fetch plugin


## Tmux resurrect
add this to `~/.tmux.conf`
```
set -g @plugin 'tmux-plugins/tmux-resurrect'
```

press `prefix , I` to fetch plguin

### usage
`prefix , ctrl+s ` save sessions
`prefix , ctrl+r ` restore sessions

### Assign restored programs+

MYSETTING:
```
set -g @resurrect-processes 'mosh-client python3'
```

Example restoring additional programs:
```
  set -g @resurrect-processes 'ssh psql mysql sqlite3'

```

Programs with arguments should be double quoted:
```
  set -g @resurrect-processes 'some_program "git log"'
```

Start with tilde to restore a program whose process contains target name:
```
  set -g @resurrect-processes 'irb pry "~rails server" "~rails console"'
```

Use `->` to specify a command to be used when restoring a program (useful if the default restore command fails ):
```
  set -g @resurrect-processes 'some_program "grunt->grunt development"'
```
- https://github.com/tmux/tmux/wiki
- terminal multiplexer like [[GNU screen]]
- ## `~/.tmux.conf`
	- ``` 
	  # Re-assigning C-b to C-a
	  unbind C-b
	  set-option -g prefix C-a
	  
	  # Bindings for C-a a
	  bind-key a send-prefix
	  
	  bind-key - split-window -v
	  bind-key \\ split-window -h
	  bind-key | split-window -h
	  
	  bind-key C-o rotate-window
	  
	  bind-key + select-layout main-horizontal
	  bind-key = select-layout main-vertical
	  set-window-option -g other-pane-height 25
	  set-window-option -g other-pane-width  80
	  
	  set-window-option -g automatic-rename off
	  set-option -g allow-rename off
	  
	  set-option -g pane-active-border fg=yellow
	  set-option -g status-left-length 32
	  set-option -g status-left '[#S:#I.#P] '
	  
	  set -g base-index 1
	  setw -g pane-base-index 1
	  
	  set-option -g repeat-time 0
	  set-window-option -g display-panes-time 1500
	  
	  set-option -g default-terminal screen-256color
	  
	  set -g mouse on
	  
	  if-shell "test -f ~/.tmux.conf.local" "source-file ~/.tmux.conf.local"
	  
	  
	  ```
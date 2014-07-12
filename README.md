# manuel_contrib_watch

A plugin for [manuel](https://github.com/ShaneKilkelly/manuel), which
watches for changes in a directory and reacts with user-defined actions


# Prerequisites

This plugin depends on the `inotify-tools` package for linux, specifically
the `inotifywait` program.


# Usage

```bash
# In a manuelfile

load_plugin manuel-contrib-watch

function do_something {
  declare -A actions=(
    ["\.js$"]="echo 'we should concat and minify the js again'"
    ["\.go$"]="go build ."
  )

  manuel_watch . actions
}
```

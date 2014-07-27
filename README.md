# manuel-contrib-watch

A plugin for [manuel](https://github.com/ShaneKilkelly/manuel), which
watches for changes in a directory and reacts with user-defined actions.

This plugin currently requires bash version 4 or higher.


# Installation

Clone this repository into your manuel plugins
directory ($HOME/.manuel.d/plugins by default):
```bash
$ cd ~/.manuel.d/plugins
$ git clone git://github.com/ShaneKilkelly/manuel-contrib-watch.git
```


# Usage

Start the `manuel_watch` task, providing a directory to watch over, and an
associative-array of regex-patterns to watch for and corresponding actions
to take when a file matchin that pattern changes.

Example:
```bash
# In a manuelfile

load_plugin manuel-contrib-watch

function wait_for_change {
  declare -A actions=(
    [".*\.js$"]="echo 'we should concat and minify the js again'"
    [".*\.go$"]="go build ."
  )

  manuel_watch . actions
}
```

The regex patterns should be compatible with the unix `find` command.
In the above example, if the file `./assets/js/app.js` changes, the first item in
the `actions` associative-array will match, and the corresponding command
string will be run.


## Changelog

### v1.0.0

- remove dependency on `inotify-tools`, making the `manuel_watch` task
  work on any unix system where `find` and either `md5` or `md5sum` are available.

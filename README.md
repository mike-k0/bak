# bak

**bak** is a command-line utility for creating and restoring backup copies of single files - `.bak` files - without clutter.

As residents of the terminal, we all make a lot of on-the-fly, in-place, single-file backups. Config files, dotfiles, "I'm only pretty sure I know what I'm doing" files, before you break them, you do this:

`cp my_thing.file my_thing.file.bak`

The problem, of course, is remembering to delete that file when you're finished.

**bak**'s goal is simply to obviate this process. Using **bak**, you'll be able to manage your bakfiles with four simple commands:

`bak my_file` - Create a bakfile in a configured location (default: XDG_DATA_HOME/bak/bakfiles, or XDG's default location)  
`bak up my_file` - Overwrite current `my_file.bak`, rather than creating a second .bakfile. 
`bak down my_file` - Deletes `my_file` and restores it from `my_file.bak`  
`bak off my_file` - Deletes `my_file.bak`, confirming by default (`bak off -q` to suppress)

Don't worry, they're easy to remember after a minute:

`bak`: bak.  
`bak up`: I've made changes, back them up.  
`bak down`: I've screwed up, undo the damage.  
`bak off`: I'm done working. Go away, **bak**, and take your .bakfile with you.

## Additional commands and flags
`bak down --keep my_file` - Restores from .bakfile, does not delete .bakfile  
`bak show my_file` View a .bakfile in $PAGER  
`bak show --using exec my_file` View a .bakfile using `exec`  (alias `--in`)

examples:

        bak show --using cat my_file.json
        bak show --in nvim my_file.json
`bak get-bak my_file` Get the abspath of a .bakfile, in case, for some reason, you want to pipe it somewhere

example:

    bak get-bak my_file.json >> xargs diff my_file.json
    (will be useless once 'bak diff' is implemented, but
     whatever.)

## Advanced features (Not yet implemented as of Oct. 28, 2020)
**bak** is also slated to support a number of flags, as well as rich output, such as:

`bak list` - List all .bakfiles, with a bit of metadata to help with disambiguation  
`bak list my_file` - List all .bakfiles *of the specified file*, with metadata  
`bak diff my_file <bakfile>` - Self-explanatory. Without .bakfile argument, diffs `my_file` against its most recent .bakfile. By default, uses [ydiff](https://github.com/ymattw/ydiff). Can be configured to use the difftool of your choice.

## Current state (updated Oct. 31, 2020)
This is a very pre-alpha version, as in, this is a spaghetti proof-of-concept. Perhaps ~~5-6~~ 12-15 hours have been spent on development so far. As such, it's only "working" in the strictest sense.

At the moment, **bak** stores its database and your bakfiles in `$XDG_DATA_HOME/bak`. If `$XDG_DATA_HOME` is not set, its specified default is used, and your stuff ends up in `~/.local/share/bak`.

If the above sections suggest that a command is implemented, it's working at the most basic level. There are few sanity checks. Expect and please report bugs, as well as feature requests. If you're brave enough to work on a project in the early, mediocre phase, go nuts with the PRs.

Also, there's ~~no~~ very little exception handling (yet.)

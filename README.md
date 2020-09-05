# Monkey on Wynton

Doing this alone? Impossible without a huge time investment. Working with a "ported" Monkey that the bioinformatics core established? Easy. Well, sort of.

Executable location on Wynton: `/wynton/group/gladstone/biocore/MonkeyPipeline/monkey_agw`

## Disclaimer

Monkey on Wynton comes with a few caveats:

1. All warnings and configuration paths are set as if this is running on Rigel - do not follow these instructions for fixes, open an issue here instead
2. Long-term support will be next to nonexistent
    - This "port" is solely to extend Monkey's life through completion of projects that previously depended on it
    - New projects should utilize new, Wynton-optimized pipelines.
    - [Contact me](mailto:angelo.pelonero@gladstone.ucsf.edu) if you need help with these - helper scripts are coming soon.
3. Monkey on Wynton has not been extensively tested, so bugs are likely (though may be rare)
4. Monkey generates an absolute boatload of log files - name your projects with a unique ID for easy log file management (to facilitate use of a command like `mv *uniqueID* logfiledir/` or similar)

## Setup

Prerequisites:

1. A Wynton account + a loose working knowledge of the system
2. Access to the Gladstone Data Transfer server [optional, but highly recommended]

Steps:

1. Add the contents of `src/add2bash_profile.txt` to the end of your Wynton account's `.bash_profile`
    - Do *not* add this to `.bashrc` unless you want to break some core server functionality!
    - Example `.bash_profile` can be found in `src/bash_profileExample4MonkeyOnWynt.txt`

2. Run `source ~/.bash_profile` or log out + bask in to activate changes
3. Invoke `monkey config.cfg` to submit jobs
    - Example config file can be found in `src/example_config_MonkeyOnWynt.cfg`
    - **IMPORTANT**: ALWAYS use `/wynton/group/gladstone/users/your-username/` for your projects.
    - NOTE: I [Angelo] am unclear on these rsync settings (URL and folder). Any long-time Monkey users care to explain this to me?


```
-={ see no Rigel }={ hear no Rigel }={ speak no Rigel }={ have mo fun }=-
       .-"-.            .-"-.            .-"-.           .-"-.
     _/_-.-_\_        _/.-.-.\_        _/.-.-.\_       _/.-.-.\_
    / __} {__ \      /|( o o )|\      ( ( o o ) )     ( ( o o ) )
   / //  "  \\ \    | //  "  \\ |      |/  "  \|       |/  "  \|
  / / \'---'/ \ \  / / \'---'/ \ \      \'/^\'/         \ '-' /
  \ \_/`"""`\_/ /  \ \_/`"""`\_/ /      /`\ /`\         /`"""`\
   \           /    \           /      /  /|\  \       /       \

-={ see no Error }={ hear no Error }={ speak no Error }={ have mo fun }=-
```
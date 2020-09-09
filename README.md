# Monkey on Wynton

Porting Monkey to Wynton on my own? Impossible without a huge time investment. Working with a ported Monkey that the Gladstone bioinformatics core established? Easy. Well, sort of.

Executable location on Wynton: `/wynton/group/gladstone/biocore/MonkeyPipeline/monkey_agw`

## Disclaimer

Monkey on Wynton comes with a few caveats:

1. All warnings and configuration paths are set as if this is running on Rigel - do not follow these instructions for fixes, open an issue here instead
2. Long-term support will be next to nonexistent
    - This "port" is solely to extend Monkey's life through completion of projects that previously depended on it
    - New projects should utilize new, Wynton-optimized pipelines.
    - [Contact me](mailto:angelo.pelonero@gladstone.ucsf.edu) if you need help with these - helper scripts are coming soon.
3. Monkey on Wynton has not been extensively tested, so bugs are likely (though may be rare)
4. Monkey generates an absolute boatload of log files - name your projects with a unique ID for easy log file management (see "Best Practices" section at bottom or README)

## Setup + Runs

#### Prerequisites:

1. A [Wynton account](https://wynton.ucsf.edu/hpc/about/join.html) + a working knowledge of the system (browse the [Wynton HPC site](https://wynton.ucsf.edu/hpc/index.html) to learn more)
2. Access to the [Gladstone Data Transfer server](https://confluence.gladstone.org/confluence/display/WYN/Moving+files+between+Gladstone+and+Wynton) [optional, but highly recommended]

#### Setup:
##### (run this once)
1. Add the contents of `src/01_setup/add2bash_profile.txt` to the end of your Wynton account's `.bash_profile`
    - **1a.** *By script:* 
        - Upload files from `src/01_setup/` to your Wynton home directory, login to Wynton, and run `sh MonkeySetup.sh`
    - **OR 1b.** *Manually:*
        - Copy the contents of `src/01_setup/add2bash_profile.txt` and paste it into your Wynton's ~/.bash_profile via your favorite text editor (login, `nano ~/.bash_profile`, paste lines, save file) + `source ~/bash_profile`)
    - Do *not* add this to `.bashrc` unless you want to break some core server functionality!
    - An example Wynton `.bash_profile` can be found in `src/_misc_info/bash_profileExample4MonkeyOnWynt.txt`

2. Test monkey by running `monkey`. You should see this output if setup was successful:

   ```
   ERROR: You must specify a "study design" file (as the very last command line argument to the program) when running Monkey. See --help for more options. at /wynton/group/gladstone/biocore/MonkeyPipeline/monkey_agw line 95.
   ```

Monkey is now ready for use. You will not need to repeat these steps.

#### Run:
NOTE 09-09-2020: I [Angelo] am unclear on these rsync settings (URL and folder). Clarification on ths would be appreciated - let me know!

Until this is clarified please [contact me](mailto:angelo.pelonero@gladstone.ucsf.edu) for advice on these settings (lines 54-55 in `.cfg` file)

1. Copy your source data to Wynton (`/wynton/scratch/your-project-dir/` or `/wynton/group/gladstone/your-username/` only)
2. Setup your source files and config document
    - An example Monkey `.cfg` document can be found in `src/02_configs/example_config_MonkeyOnWynt.cfg`
    - A blank config can be found in `src/02_configs/MonkeyonWyntConfig.cfg`
3. `cd` to the project directory
4. Invoke `monkey config.cfg` to run Monkey
5. Let the script run and return ou to the command line (warnings are OK, errors will stop job submission)
6. Check job status with `qstat` - you can exit Wynton and let these processes run.
7. Move results and source data to Dropbox or the Hub - `scratch` is wiped regularly and `group/` has finite space! Be a good citizen.

##### Best practices:
- ALWAYS use `/wynton/scratch/your-project/` OR `/wynton/group/gladstone/users/your-username/` for your work. Create a directory if you do not have one, and always move your source files and Monkey outputs off of Wynton after a run.
- **Again, do NOT store your source data or results on Wynton.** Please remove all files at the end of a run and store them on Dropbox/the Hub.
- Use care when manipulating job log files in your home directory.
    - Name your projects with a unique ID for easy log file management. As an example:
        - [in monkey.cfg]: `studyName = UniqueID115566`
    - After your run, you will see loads of log files in your home dir (`~/`) - `UniqueID115566_processname.e[JOB_ID]`, `UniqueID115566_processname.o[JOB_ID]`, etc.
    - You can batch move or delete these files like so: `mkdir logfiledir | mv UniqueID115566* logfiledir/` or `rm UniqueID115566*`

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

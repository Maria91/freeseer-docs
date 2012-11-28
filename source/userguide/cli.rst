CLI
===

CLI Basics
----------

The CLI in a alternative to using the GUI for recording and changing config settings for Freeseer. This tool is easy to use and has been made to be as user friendly as possible.

The CLI allows Freeseer to be run entirely on the command line. It contains the same basic featrues. Commands that are implemented include help, config, talk, and record.

To run the CLI:
1. Run **./src/freeseer-cli**

To exit the CLI:
1. Run **exit**
2. Run **quit**

To view license and credits:
1. Run **credits**
2. Run **license**

Recording
**********

To record:

1. run **record <id>**
2. When end recording press **<space>**

This will record the video using the current configurations.

Checking Config Settings
************************

To view config settigs:

1. run **config show <setting>**

Available Settings:
...................
1. Video
2. VideoMixer
3. VideoInput
4. Audio
5. AudioMixer
6. AudioInput
7. All

Changing Config Settings
************************

To change config settings:

1. For Video **config set VideoMixer <option> <Input option> <plugin>**
2. For Audio **config set AudioMixer <option>**
3. For directory **config set dif <path>**
4. For file **config set file [on|off]**
5. For streaming **config set streaming [on|off]**

Talk
****

This setting is used to manage talks, it is possible to add, remove or update talks as well as to view existing talks. 

To use talk:
1. run **talk <command>**

Available Commands
..................
1. show all
2. show events
3. show <mode> <id>
4. remove <id>|all
5. add
6. update <id>

Available Modes
...............
1. Event
2. Id
3. Room

Help
****

The help command has been made to be self explanatory. Each step shows you the next possible option if you need more indepth help.

Options for  help:
1. run **help**
2. run **help <command>**
3. run **help <command> <arguments>**


Common Problems
...............
1. Make sure you are in the correct directory
2. Case matters for the first command, it must be lowercase. 


***Now maintained on Github:*** [https://github.com/WMFO/Rivendell-Spinitron-Update](https://github.com/WMFO/Rivendell-Spinitron-Update "https://github.com/WMFO/Rivendell-Spinitron-Update")

About
-----

This is a Rivendell loadable module made to report the current playing song to Spinitron. It was made for Rivendell 1.5. It is Free software licensed under GNU GPL version 2. Download and compile the attached file to use.

Consult the Rivendell documentation for more information on teh Rivendell RLM SDK. Some info can be found [here](http://rivendell.tryphon.org/wiki/index.php/Rivendell_Loadable_Module_(RLM)_SDK_-_For_Sending_Now_%26_Next_Data_to_external_systems "http://rivendell.tryphon.org/wiki/index.php/Rivendell_Loadable_Module_(RLM)_SDK_-_For_Sending_Now_&_Next_Data_to_external_systems").

Please note: when the on-air signal is on, the module posts to the current playlist of the active Spinitron user; when it is off, it posts to the account provided in the parameters. This was made to support automated playback when no 'live' Spinitron user is logged in. It effectively logs all automated playlists under a 'fake' automated user. This user should be set up in Spinitron just like a regular user. We use a Macro cart on the Rivendell cart screen to turn Automation 'on' or 'off' and switch between the active DJ and the automation user.

For questions or to contribute, contact: [ops@wmfo.org](mailto:ops@wmfo.org "mailto:ops@wmfo.org")

Comments
--------

/\*

 \*  rlm\_spinitron.c

 \*  

 \*  Module by Eric Berg, Benjamin Yu (C) Copyright 2009.

 \*

 \*   This program is free software; you can redistribute it and/or modify

 \*   it under the terms of the GNU General Public License version 2

 \*   as published by the Free Software Foundation.

 \*   

 \*   This program was created as a simple way for metadata to be logged

 \*   in the Spinitron system.

 \*

 \* This is a Rivendell Loadable Module.  It sends Now&Next PAD data via

 \* UDP packets to the destination(s) specified in the configuration file 

 \* pointed to by the plugin argument.

 \*

 \* To compile this module, just do:

 \* 

 \*   gcc -shared -o rlm\_spinitro.rlm rlm\_spinitron.c -Wall -Werror -fPIC

 \*

 \*/

Notes:
------

Username and password hard-coded in (So, it's a little hacked together.). To set them for your station, find and change the following fields before compiling the file:

\<YOUR\_ACCOUNT\_HERE\>

\<PASSWORD\>

\<YOUR\_STATION\_ID\_HERE\>

Changelog:
----------

8-11-10 - Original Upload

1.  1. [About](#About)
2.  2. [Comments](#Comments)
3.  3. [Notes:](#Notes:)
4.  4. [Changelog:](#Changelog:)

[Page Attachments](https://wiki-files.wmfo.org/Operations/Station_Architecture_Overview/Code/Rivendell_-_Spinitron_Update)

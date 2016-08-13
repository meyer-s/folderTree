***Now maintained on GitHub:***

Version 1: [https://github.com/WMFO/WMFO-Lyric-Flagger](https://github.com/WMFO/WMFO-Lyric-Flagger "https://github.com/WMFO/WMFO-Lyric-Flagger")
 Version 2: [https://github.com/WMFO/WMFO-Lyric-Flagger-v2](https://github.com/WMFO/WMFO-Lyric-Flagger-v2 "https://github.com/WMFO/WMFO-Lyric-Flagger-v2")

Makes use of [Profanity detecting regex](https://wiki.wmfo.org/Operations/Code/Profanity-Detecting_Regex "Profanity-Detecting Regex") file.

Version 2
---------

In operation as of 2011. See [github](https://github.com/WMFO/WMFO-Lyric-Flagger-v2 "https://github.com/WMFO/WMFO-Lyric-Flagger-v2") for more info.

Version 1
---------

### A Note on LyricsFly

This program uses the LyricFly API. For more information, or to obtain a permanent user key, please visit [http://lyricsfly.com/api/](http://lyricsfly.com/api/ "http://lyricsfly.com/api/").
 Update: *The lyricsfly API appears to have been discontiued. Version 2 of the LyricsFlagger does not requrie it.*

### LyricsGrabber

namespace lyricGrabber contains code to grab lyrics of songs from various internet sites. The only external function called should be list\<string\>\* getLyrics(string title, string artist, string album).

### LyricsChecker

Class LyricChecker performs lyric checks and returns the number of matchs found.

1.  1. [Version 2](#Version_2)
2.  2. [Version 1](#Version_1)
    1.  2.1. [A Note on LyricsFly](#A_Note_on_LyricsFly)
    2.  2.2. [LyricsGrabber](#LyricsGrabber)
    3.  2.3. [LyricsChecker](#LyricsChecker)



These instructions have you use FTP, but scp, ssh and a unix text editor (emacs, vim) will work just as well. If you are unsure of any step, keep a copy of the original.

To change the side banner on wmfo.org follow these steps:

1.  If it's a new banner, upload it to the /wmfo.org/banners directory on the ftp server ([credentials here](https://wiki.wmfo.org/Operations/Credentials/Hosting_Credentials "Hosting Credentials")). **Make sure banner is 188 px wide!**
2.  Download rightbar.php from \~/wmfo.org/wp-content/themes/wmfo/rightbar.php
3.  Change the image filename, href, title (mouseover) and alt (description for screen readers).
4.  Upload rightbar.php back up to the site, overwriting the old version.
5.  Test and make sure it works.

*

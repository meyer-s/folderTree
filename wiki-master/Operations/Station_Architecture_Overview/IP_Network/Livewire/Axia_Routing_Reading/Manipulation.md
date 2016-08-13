Without the official proprietary docs, here are some examples on Axia node manipulation determined through analyzing the HTML forms on the site:

    $ curl -s -u user:password http://192.168.0.110/cgi-bin/cgi_dsts | grep "name=R007_RURL" | grep -c 10500
    1
    $ echo $?
    0
    $ curl -s -u user:password http://192.168.0.110/cgi-bin/cgi_dsts | grep "name=R007_RURL" | grep -c 13500
    0
    $ echo $?
    1

Thus, you can query the routing selecting. The query above will tell you whether or not Studio A is on-air (10500 is PGM1 from the Studio Engine).

    curl -u user:password --data "cmd=set&R001_RURL=10500" http://192.168.0.110/cgi-bin/cgi_dsts

This query will set Input 2 on the COND1 to Axia channel 10500.

*

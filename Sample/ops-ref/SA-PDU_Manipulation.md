For SAPDU1, you can manipulate outlets with the following schema:

Telnet
------

    <?php
    $pdu=fsockopen("tcp://192.168.1.20","23",&$errno,&$errstr);
    if(@$argv[1]){
            $outlet = $argv[1];
            switch($argv[2]) {
                    case "on":
                            $res = 1;
                            break;
                    case "off":
                            $res = 2;
                            break;
                    case "reboot":
                            $res = 3;
                            break;
                    default:
                            die("invalid action\n");
                            break;
            }
    $sequence= "user\r\nPASSWORD\r\n1\r\n3\r\n" .$outlet. "\r\n1\r\n" .$res. "\r\nYES\r\n^[^[^[^[\r\n4\r\n";
    $result=fwrite($pdu,$sequence);
    if($outlet>8||$outlet<1){
    die("Invalid outlet\n");
    }
    } else{
    echo "Usage: ${argv[0]} OUTLET {on,off,reboot}\n";
    }
    fclose($pdu);

 

cURL

    curl --data "OL_Cntrl_Col1_Btn=?OUTLET,2&rPDUOutletCtrl=OPERATION" -u user:PASSWORD http://192.168.1.20/Forms/rPDUout1

    curl -u user:PASSWORD http://192.168.1.20/rPDUoconf.htm

    curl --data "Control=" -u user:PASSWORD http://192.168.1.20/Forms/rPDUoconf1


    curl -u user:opsteam http://192.168.1.20/rPDUout.htm

**OPERATIONs**: 2-ON, 4-OFF, 6-Reboot

**OUTLET** should be the outlet number plus one (so outlet 8 is 9...don't ask why...)

And yes, you have to download the rPDUoconf.htm page or else it rejects the final confirmation command.

The final command allows you to view the status of all the outlets.

1.  1. [Telnet](#Telnet)


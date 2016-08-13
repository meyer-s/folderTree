 

The donations website (Ver 3) is based upon previous work by Andy Saylor and Ben Yu and has been updated to use Twitter Bootstrap, MySQLi, and a little jQuery. The WMFO Donations website centers around the SallieMae platform (however much we dislike it). The donation flow

1.  index.php
2.  options.php
3.  wmfolog.php
4.  SallieMae Portal
5.  thankyou.php or cancel.php

is based upon posting to SallieMae, and a post back script receives the information back from payments.

 

Generally
---------

All pages pull from head.inc.php which defines the header and navigation links.

### index.php

This page starts the donation flow. Inputs are required with the HTML5 required tag which does not work in IE9. There are two PHP arrays which define the text for the donation value links and popover bubbles. The bottom text is defined in typical paragraph form. This page posts all fields to options.php, which prints each field in a hidden HTML form input.

 

### options.php

(accessed only through index.php)

This page receives all information from index.php and should not be accessed directly except in testing. The typeahead on this page pulls data from schedule.wmfo.org hosted on Duke. There is a page on duke (titled donations something) which spits out all the shows on schedule.wmfo.org into an array which can be interpreted by the bootstrap typeahead. Two additional (All of them and None) are typed in manually on options.php. All information on this page is posted to wmfolog.php.

 

### wmfolog.php 

(page not viewed. stores POST data from options.php and POSTs to TouchNet)

This page firsts dumps the necessary post data into the WMFO database in mysql.wmfo.org. It loads a hidden form on the page. Onload, javascript on the page automatically submits the form which POSTs the data contained in hidden form elements according to TouchNet's specifications (which are populated by the php script from the POST data received from options.php) to the salliemae URL.

As it inserts into the database, it fetches the ID of the field and places it into the ACCOUNT post field to the SallieMae database. The ACCOUNT\_EDT is set to N to prevent people from altering the account number on SallieMae. This number is used to validate the post back.

### SallieMae Portal

This receives our post data and behaves accordingly. Currently, we post data to not allow changing of certain parameters such as cost and ACCOUNT ID field. This allows us to prevent the user doing things like changing the payment down on the final portal and eliminates any confusion.

### postback.php

This page receives the SallieMae post back from its validation process. This allows us to validate whether a payment actually took place (uhhh...). It then inserts this data into the \`postback\` table on mysql.wmfo.org donations database.

 

### stats.php

This page generates the HTML content for the sidebar used on the main website, including most recent donor, total amount raised, and the first 4 show leader boards. These are fairly complex SQL queries, so don't touch unless you're willing to do a little playing.

 

### results.php

This page allows pulling of detailed (but obfuscated) results about the donation drive, including viewing the full show leader board, the individual pledge leader board, and querying of donation first names and values by show.

This uses jQuery to automatically update the table when the form fields are changed, and pulls from resultstable.php to populate the table HTML.

### thankyou.php

Upon successful payment and clicking continue, you're forwarded to this page that says thankyou with a link back to the homepage.

### cancel.php

Upon hitting the cancel button on SallieMae's portal, you get dropped to this page with a link to start donation process over.

1.  1. [Generally](#Generally)
    1.  1.1. [index.php](#index.php)
    2.  1.2. [options.php](#options.php)
    3.  1.3. [wmfolog.php ](#wmfolog.php)
    4.  1.4. [SallieMae Portal](#SallieMae_Portal)
    5.  1.5. [postback.php](#postback.php)
    6.  1.6. [stats.php](#stats.php)
    7.  1.7. [results.php](#results.php)
    8.  1.8. [thankyou.php](#thankyou.php)
    9.  1.9. [cancel.php](#cancel.php)



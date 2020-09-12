# File Inclusion
File inclusion is a web app vulnerability which allows any visitor to load & view restricted files on the website
  - ### Local File Inclusion (LFI)
    - when local & restricted file (i.e file on same site) can be loaded, It's vulnerable to LFI. 
  - ### Remote File inclusion (RFI)
    - when remote file from another domain can be loaded, It is vulnerable to RFI.
    
## How to identify _File Inclusion Vulnerability_    
> If you can read any of these files

    /etc/passwd
    /etc/profile
    /etc/issue
    /proc/version
    /etc/profile
    /etc/passwd
    /etc/passwd
    /etc/shadow
    /root/.bash_history
    /var/log/dmessage
    /var/mail/root
    /var/spool/cron/crontabs/root

> :shipit: Attacker will try to find way to write mal code onto system files like

    /proc/self/environ
    /var/log/auth.log
    /var/log/apache2/access.log
 
 > RFI is only vulnerable if PHP setting of ***allow_url_fopen*** and ***allow_url_include*** is set to ***On***
  
 ## Google dorks for LFI
 
    allinurl:pgg=contact.php
    allinurl:page=contact.php
    allinurl:home=contact.php
    allinurl:?index.php?pagina=contato.php site:br
    allinurl:?index.php?pagina=clientes.php site:br
    allinurl:?index.php?pagina=produtos.php site:br
    allinurl:?index.php?pagina=contato.php


    index.php?pagina=home.php
    index.php?pagina=empresa.php
    index.php?pagina=obras.php
    index.php?pagina=localizacao.php
    index.php?pagina=contato.php
    thumb.php

    index.php?pagina=empresa.php
    index.php?pagina=produtos.php
    index.php?pagina=representantes.php
    index.php?pagina=contato.php
    index.php?pagina=home.php
    index.php?pagina=guia_consumidor.php
    index.php?pagina=responsabilidade.php

    inurl:"?page=news.php"
    inurl:"index.php?main=*php"
    inurl:"index.php?inc=*php"
    inurl:"index.php?pg=*php"
    inurl:"index.php?include_file=*php"
    inurl:"index.php?main=*html"
    inurl:"index.php?inc=*html"
    inurl:"index.php?pg=*html
    inurl:index.php?id=
    inurl:index.php?cat=
    inurl:index.php?action=
    inurl:index.php?content=
    inurl:index.php?page=

## Google dorks for RFI

    inurl:rte/my_documents/my_files
    inurl:/my_documents/my_files/
    inurl:/shoutbox/expanded.php?conf=
    inurl:/main.php?x=
    inurl:/myPHPCalendar/admin.php?cal_dir=
    inurl:/index.php/main.php?x=
    inurl:/index.php?include=
    inurl:/index.php?x=
    inurl:/index.php?open=
    inurl:/index.php?visualizar=
    inurl:/template.php?pagina=
    inurl:/index.php?pagina=
    inurl:/index.php?inc=
    inurl:"index.php?page=contact.php"
    inurl:"template.php?goto="
    inurl:"video.php?content="
    inurl:"pages.php?page="
    inurl:"index1.php?choix="
    inurl:tinybrowser/upload.php
    inurl:examples/uploadbutton.html
    inurl:/modules/mod_mainmenu.php?mosConfig_absolute_path=
    inurl:/include/new-visitor.inc.php?lvc_include_dir=
    inurl:/_functions.php?prefix=
    inurl:/cpcommerce/_functions.php?prefix=
    inurl:/modules/coppermine/themes/default/theme.php?THEME_DIR=
    inurl:/modules/agendax/addevent.inc.php?agendax_path=
    inurl:/ashnews.php?pathtoashnews=
    inurl:/eblog/blog.inc.php?xoopsConfig[xoops_url]=
    inurl:/pm/lib.inc.php?pm_path=
    inurl:/b2-tools/gm-2-b2.php?b2inc=
    inurl:/modules/mod_mainmenu.php?mosConfig_absolute_path=
    inurl:/modules/agendax/addevent.inc.php?agendax_path=
    inurl:/includes/include_once.php?include_file=
    inurl:/e107/e107_handlers/secure_img_render.php?p=
    intitle:index of? inurl:kindeditor

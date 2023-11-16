# Zakázať prístup k wp-login, wp-admin, wp-json a XML-RPC v .htaccess:

## Prerekvizity

1. Je potrebné mať SSH prístup na server, na ktorom je prevádzkované Vaše webové sídlo s inštanciou Content Management System (CMS) Wordpress.
2. Je potrebné mať práva na zápis do súboru `.htaccess` v koreňovom adresári Vášho systému využívajúceho CMS Wordpress.
3. Tieto akcie často vykonáva správca webu. 
4. Vzhľadom na aktivity vykonávané útočníkmi odporúčame vypnúť prístup k nasledujúcim súborom pomocou úprav v súbore s `.htaccess`.

## 1. Zakázať prístup k wp-login.php, wp-admin a ďalším súborom:

Ak chcete zakázať prístup nielen k `wp-login.php`, ale aj k `wp-admin` a ďalším súborom, použite tento kód:

    <FilesMatch "^(wp-login\.php|wp-admin/)">
      Order Deny,Allow
      Deny from all
      Allow from xxx.xxx.xxx.xxx
    </FilesMatch>

Týmto spôsobom obmedzíte prístup nielen k `wp-login.php`, ale aj k akémukoľvek súboru alebo adresáru začínajúcemu s `wp-admin/`.

## 3. Zakázať prístup k wp-json

Pridajte nasledujúci kód pre zakázanie prístupu k `wp-json`:

    # Zakázať prístup k wp-json/
    <IfModule mod_rewrite.c>
      RewriteEngine On
      RewriteCond %{REQUEST_URI} ^/wp-json/ [NC]
      RewriteRule ^(.*)$ - [R=403,L]
    </IfModule>

## 3. Zakázať prístup k XML-RPC

Ak chcete zakázať XML-RPC, pridajte nasledujúci kód:

    # Zakázanie prístupu XML-RPC
    <Files xmlrpc.php>
      Order Deny,Allow
      Deny from all
    </Files>

Uistite sa, že nahradíte `xxx.xxx.xxx.xxx` svojou skutočnou IP adresou alebo rozsahom adries (napríklad `192.168.0.10` alebo `192.168.0.0/24`). 
Predtým, než urobíte tieto zmeny, uistite sa, že máte prístup k serveru a máte zálohu svojho súboru `.htaccess`. Testujte tieto zmeny na testovacom prostredí pred aplikovaním na živý web, aby ste predišli možným problémom.

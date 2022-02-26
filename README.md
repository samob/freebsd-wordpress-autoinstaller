Še ena bash skripta namenjena avtomatizaciji WordPress namestitve za FreeBSD.

Skripta je testirana na naslednjih različicah: 12.1, 12.2. Razvijalec prosi za povratne informacije, če vam je uspelo na drugih različicah.

### Ta skripta bo avtomatično namestila svežo kopijo WordPress, skupaj z vsemi predzahtevami (PHP7.4/Apache24/MariaDB10.3) za vaš FreeBSD box. Deluje v ječah (Jails), virtualnih sistemih (VMs) in namestitvah na fizične strežnike.
> Apache in MariaDB poslušata na privzetih vratih (default ports), tako da če preusmerjate vrata v vaši ječi/VMs na ista vrata na katerih posluša gostitelj, je potrebna ročna nastavitev konfiguracije, da bo ustrezala vašemu okolju.

#### Prvi korak je, da poženete naslednji ukaz, ki bo namestil potrebne pakete in nastavil "bash" za vašo privzeto ukazno lupino.
```
pkg update -f && pkg install -y bash curl && chsh -s bash root
```

#### Naslednji potrebni korak je, da se odjavite in ponovno prijavite v sistem, da se podosobi ukazna lupina v "bash", nato poženemo naslednjo vrstico. Prijavljeni morate biti kot root uporabnik, *sudo* v tej različici ni podprt.
For FreeBSD 12:<br>
```
curl -s https://raw.githubusercontent.com/samob/freebsd-wordpress-autoinstaller/main/wordpress-installation-freebsd12.sh | bash -
```

#### Nekaj opomb:
- All WordPress files are here: <code>/usr/local/www/apache24/data/</code>
- Apache2 config file is here: <code>/usr/local/etc/apache24/httpd.conf</code>
> There is also <code>/usr/local/etc/apache24/httpd.conf.BACKUP</code>, in case you'd like to check the defaults, add more modules, etc.
- To apply any PHP.INI settings, edit <code>/usr/local/www/apache24/data/.htaccess</code> and follow the example there.
- The installation includes WP-CLI. To run a command with WP-CLI, it must start this way:<br>
```
sudo -u www wp THEN_YOUR_OPTIONS_HERE
```
- The installation is designed to be placed behind a HTTPS reverse proxy, like NGINX or HAProxy. REMOTE IP Apache module is installed and configured. WP-CONFIG.PHP is also slightly altered to play nicely with HTTPS reverse proxy.
- Only HTTPS(443) port is active, to encrypt traffic between the proxy and backend.
- All the default WordPress resoruces are removed upon login. You'll get a cleanest WordPress installation you can think of.

> Disclamer: I am not a superhuman-sysadmin, although I am always trying to keep up with the best practices, I could still make a mistake somewhere, because of that Apache2/PHP74/MariaDB10.3 may have some weak points in it's config. Open an issue and I'll fix everything ASAP. Also, if your WordPress installation requires an additional PHP module, kindly let me know, and I'll add it to the list. Thank you.

<br>
<hr>

#### Consider donating to support a quicker release of new content :)
https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=BYZMNVH4QH3L2&source=url

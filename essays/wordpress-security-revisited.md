# WordPress Security, Revisited: What I'd Change a Decade Later

*Luciano Ferrari*

In 2016 I wrote an article for Hakin9 Magazine on securing WordPress. At the time WordPress ran roughly a quarter of the web, plugins were the soft underbelly, and most site owners were still logging in over plain HTTP. The advice was practical: force TLS, lock down file permissions, stop using FTP, hide the version string, put phpMyAdmin behind something, back up, and run a vulnerability assessment against the OWASP Top 10.

Ten years on, WordPress runs an even larger share of the web, and I still get asked about it, usually by small businesses and by the marketing teams inside large ones who own a site that security never sees. Rereading the piece, some of it has aged well and some of it I would now actively argue against. Here is the updated version.

## What aged well

**Plugins are still the attack surface.** The core project has had automatic security updates for years and a mature disclosure process. The overwhelming majority of real-world WordPress compromises still come through a vulnerable or abandoned plugin or theme. The 2016 advice stands: fewer plugins, from maintained sources, kept current, and removed (not just deactivated) when no longer needed.

**Least privilege on the filesystem.** Directories 755, files 644, `wp-config.php` tighter still, never 777. Boring and correct.

**Backups are the ransomware control.** I wrote that before ransomware became the dominant threat model for small organizations. It is more true now. The one thing I would add: test the restore, and keep at least one copy somewhere the web server's credentials cannot reach.

**Assess, don't assume.** A periodic scan against the OWASP Top 10, plus WordPress-specific checks (WPScan is the standard tool), remains the fastest way to find out what an attacker already knows about you.

## What I'd change

**Stop paying for certificates and stop needing a dedicated IP.** In 2016 I listed commercial certificate authorities and explained that TLS required a dedicated IP address. Let's Encrypt and SNI made both obsolete. There is no longer any excuse for a WordPress site without HTTPS, and `FORCE_SSL_ADMIN` is a floor, not a goal: the whole site should be TLS-only with HSTS, and most hosts now do this by default.

**Stop hiding the version string.** I spent several paragraphs on removing the generator tag and cloaking the login page with a secret word in the URL. That is security by obscurity, and it buys almost nothing: scanners fingerprint WordPress from a dozen other signals, and attackers do not check the version before trying an exploit, they just try it. The effort is better spent on the control that actually works, which is being up to date.

**Make MFA the first control, not a footnote.** My 2016 plugin list ended with a Google Authenticator plugin as an afterthought. Credential stuffing and password spraying against `wp-login.php` and `xmlrpc.php` are now the most common attacks against WordPress admin accounts. Multi-factor authentication for every administrator account is the single highest-value change most sites can make, and passkey support is now available through plugins and some hosts.

**Disable what you don't use.** XML-RPC should be off unless you specifically need it. The REST API user enumeration endpoint should be restricted. File editing from the dashboard (`DISALLOW_FILE_EDIT`) should be disabled so a compromised admin account cannot drop a web shell through the theme editor.

**Treat hosting as a security decision.** In 2016 I assumed you were managing your own server over SSH. Most WordPress sites today should be on managed hosting that handles patching, WAF, malware scanning, isolation, and backups as part of the service. For a small organization, choosing a reputable managed host is a better security investment than any plugin, and it moves a whole class of operational controls to people who do them all day.

**Put a WAF and rate limiting in front.** A cloud WAF or CDN layer absorbs the brute-force noise, blocks the known-bad request patterns, and hides the origin. In 2016 this was an enterprise feature; now it is a checkbox on a free tier.

**Monitor the admin, not just the server.** An activity log of logins, plugin installs, user role changes, and file modifications is how you find out an account was compromised before the defacement or the SEO spam does. That category of plugin existed in 2016; it is essential now.

## The part that didn't change at all

The closing argument from the original article is the one I would keep word for word in spirit: there is no single plugin, setting, or product that makes a site immune. Security is layered, it is based on risk and probability, and it is a process rather than a project. WordPress has simply made that lesson cheaper to learn, because the platform is popular enough that the attackers are fully automated and the tooling to defend it is mature and mostly free.

If you run a WordPress site and want a ten-minute checklist, it is this: HTTPS everywhere, MFA on every admin, auto-updates on, fewer plugins, XML-RPC and file editing off, a WAF in front, backups you have actually restored, and an activity log you actually read.

---

*The original article, "WordPress Security," appeared in Hakin9 Magazine in July 2016.*

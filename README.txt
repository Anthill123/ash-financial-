livemy.app — export of your projects (account contact@ash-financial.com)
Prepared: 2026-11-23

This export contains two projects:

1) ASH Financial — www.ash-financial.com
   (vh-prod-main-5e2352-762b3e42.livemy.site)

   vh-prod-main-5e2352-762b3e42-files-20261123.tar.gz
       All website files as they are live today:
       home/appuser/app/        the website (index.html, chat/, resources/, assets/, icons,
                                sitemap.xml, robots.txt, site.webmanifest)
       home/appuser/*.bak-*     earlier versions of index.html saved as backups before
                                each change (Sep–Nov 2026), and other edit backups
       etc/nginx/sites-available/app.conf   the web server configuration
       To host the site anywhere: upload the contents of home/appuser/app/ to any
       static web hosting (or set it as the nginx root). No build step is needed.

   vh-prod-main-5e2352-762b3e42-image-20261123.tar.gz
       Full machine image of the server (Ubuntu 22.04 container), see "Machine images" below.

   Database: this project does not have a database. The site is static. Leads from the
   website forms were delivered by FormSubmit.co to contact@ash-financial.com and copied
   to your Google Sheet through your Google Apps Script — both are in your own accounts
   and are not affected by the shutdown.

2) ASH.AI manifest
   (vh-prod-main-724ba7-2fb3d4c0.livemy.site)

   vh-prod-main-724ba7-2fb3d4c0-files-20261123.tar.gz
       home/appuser/app/        your original upload (manifest.json, packageMetadata.json,
                                color.png, outline.png — the Microsoft Teams / Copilot Studio
                                app package)
       home/appuser/app/site/   the installable chat page (PWA) that was live on the site
       home/appuser/icongen/    the script used to generate the PWA icons
       etc/nginx/sites-available/app.conf

   vh-prod-main-724ba7-2fb3d4c0-image-20261123.tar.gz
       Full machine image of the server.

   Database: none. The chatbot itself runs on Microsoft Copilot Studio.

Machine images
--------------
The *-image-*.tar.gz files are complete server backups in the standard LXD format
(metadata version 1), restorable on LXD or Incus:

    lxc import vh-prod-main-5e2352-762b3e42-image-20261123.tar.gz ash-financial
    lxc start ash-financial
    (tested on LXD 6.10; Incus uses the same format: incus import ... / incus start ...)

If you do not use LXD/Incus, the archive is a regular tar file: the complete server
filesystem is inside backup/container/rootfs/.

If the import or start fails: the image only expects the standard "default" profile with
a network interface (eth0) and a root disk. Attach your own network with
    lxc config device add <name> eth0 nic network=<your-bridge>
and open a shell without SSH with: lxc exec <name> -- bash

For security, we removed our hosting platform's own components from the images: the
platform agent, its access tokens, the internal network (VPN) keys and our support SSH key.
They only worked inside our infrastructure. Nothing belonging to your projects was removed.
To log in over SSH after restoring, add your public key to
/home/appuser/.ssh/authorized_keys (user appuser, key-based login only).

Checksums
---------
SHA256SUMS.txt lists the SHA-256 checksum of every file. Put it in the same folder as the
downloaded files (keep the original file names) and run:
    Linux:    sha256sum -c SHA256SUMS.txt
    macOS:    shasum -a 256 -c SHA256SUMS.txt
    Windows:  Get-FileHash <file> -Algorithm SHA256   (PowerShell; compare with the list)

---
layout: post
title:  "Reload PostgreSql configs"
date:   2015-01-27 10:30:11
categories: postgresql linux terminal
---
If you are making modifications to the Postgres configuration file postgresql.conf (or similar), and you want to new settings to take effect without needing to restart the entire database, there are two ways to accomplish this.

 - **Option 1**: From the command-line shell 
`sudo -u postgres /usr/bin/pg_ctl reload`

 - **Option 2**: Using SQL 
`SELECT pg_reload_conf();`

Using either option will not interrupt any active queries or connections to the database, thus applying these changes seemlessly.
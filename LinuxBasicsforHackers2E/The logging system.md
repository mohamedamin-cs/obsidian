`journalctl` : display all the log entries on your screen
priority : `journalctl –p ″emerg″` emerg (0) alert (1) crit (2) err (3) warning (4) notice (5) info (6) debug (7)
`sudo journalctl –u apache2 –-vacuum-time=1d` : delete all logs
`shred` will delete the file and overwrite it several times
`shred -f -n 10 /var/log/journal/subdirectory name*.*` : -f change permission / -n ahow many times overwrite
to disable logging open `/etc/systemd/journald.conf` and set `Storage=null` then `sudo systemctl restart system-journald`

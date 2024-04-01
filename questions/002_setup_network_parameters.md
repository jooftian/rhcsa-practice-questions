# Setup network parameters
## Question:
Please create new network connection using provided values:
| Parameter   | Value              |
| ----------- | ------------------ |
| IP          | xxx.xxx.xxx.xxx/yy |
| Gateway     | zzz.zzz.zzz.zzz    |
| DNS server  | aaa.aaa.aaa.aaa    |
| Interface   | ethX               |
***
(scroll down for an answer)
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

## Answer 1 - NetworkManager CLI (`nmcli`):

We use the Network Manager CLI (nmcli) to perform this action, as it is faster.
Issue following command to set the new connection data (We assume interface type is ethernet as its name is `ethX`):
```
nmcli conn add con-name MY_CONNECTION ifname eth0 type ethernet ipv4.method manual ip4.addresses xxx.xxx.xxx.xxx/yy ipv4.gateway zzz.zzz.zzz.zzz ipv4.dns aaa.aaa.aaa.aaa
```
The previuos command creates a new connection for a specific interface. However, if we want to modify an exisiting connection issue the following command.
```
nmcli con mod MY_CONNECTION [+]ipv4.dns aaa.aaa.aaa.aaa
nmcli con mod MY_CONNECTION ipv4.ignore-auto-dns yes # to disable DHCP DNS
```
> Notice the `[+]` in the command: if used with `+`, provided DNS will be **added** to the list of DNS being used. If omitted, the whole list will be **replaced** by 
provided value.

At the final stage it is wise to start this connection:
```
nmcli con show --active      # to check if the connection is not up 
nmcli con up MY_CONNECTION
nmcli con show --active      # to check if the connection is up
```

If asked to automatically start the new connection on system reboot:
```
# Disable the old connection from starting on reboot 
nmcli con mod OLD_ACTIVE_CONNECTION connection.autoconnect no

# Automatically switch to new connection on reboot 
nmcli con up MY_CONNECTION connection.autoconnect yes
```
  
## Answer 2 - NetworkManager TUI (`nmtui`)
1. Issue the comand `nmtui` with a privileged user or with `sudo` to access the NetworkManager TUI. You can navigate the TUI with the Arrow keys, select with Enter or Space and exit with ESC.
2. In the *NetworkManager TUI* window (main window of the TUI), select *Edit a connection*. In the new screen, to the right, select *Add*. In the *New Connection* window, select *Ethernet*. The following actions are performed in the new *Edit Connection* window.
5. Place the cursor over the textbox besides *Profile name* and change it to the desired profile name (`MY_CONNECTION`). Likewise, fill the *Device* field with `ethX`.
6. In the *IPv4 CONFIGURATION* field, change from *\<Automatic>* method to *\<Manual>* method by selecting the method and changing it in the prompted window. Then select *\<Show>* to the right. New configuration fields are now shown.
7. In the *Addresses* field, press enter then input the IP address and mask `xxx.xxx.xxx.xxx/yy`.
8. In the *Gateway* field, input the gateway IP `zzz.zzz.zzz.zzz`
9. In the *DNS servers*, press enter then input the IP address of the DNS `aaa.aaa.aaa.aaa`
10. Enssure the *Automatically connect* option is active if it's required for the connection to start on system boot.
11. To finalize, select *\<OK>*. You are back to the connection selection screen.
12. Press ESC or select *\<Back>* to return to the *NetworkManager TUI* window.
13. Select *Activate a connection*. In the new screen, search your newly created ethernet connection. If it's active, for good meassure, deactivate and reactivate the connection by pressing Enter twice over the connection. If it's not, activate the connection by pressing Enter once. Press ESC or select *\<Back>* to return to the main screen. Connection status: if there is an asterisk (*) to the left of a connection, it is active.
15. We're done! Select *Quit* or press ESC to exit the NetworkManager TUI.

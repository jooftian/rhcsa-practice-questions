# Change hostname

## Question
Change hostname of the system

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

## Answer
Actually there are numerous ways to achieve that
* The simplest one is to use `nmtui` and choose proper item in the menu.
* You can manually edit `/etc/hostname` (Not recommended).
* It is possible to use the command `hostnamectl`.
* It is possible to use `nmcli` for this.

```
hostnamectl set-hostname SOME_NAME
nmcli general hostname SOME_NAME
```

While the hostname has already changed, the input prompt may not reflect the change until the connection to the host is restarted.

## Additional comment
Of course the hostname is shown near input prompt in the console, however there is also a couple of ways to obtain it: 
* Using `hostnamectl`, which besides info about hostname gives a lot of other useful information (hostnamectl(1)).
* Using `nmcli general hostname` returns the hostname.
* Using the command `hostname` (hostname(1). Can also change the hostname, but the change is only temporary).
* Using `cat /etc/hostname`.

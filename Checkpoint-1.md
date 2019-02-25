# Checkpoint 1

Everything in between angle brackets <> are meant to be filled in.

## Preperation

To start you will probably need a VPN connection to school. You can do that with [this link](https://ikdoeict.freshdesk.com/support/solutions/articles/31000136666-howto-verbinding-maken-naar-het-schoolnetwerk-via-vpn). Also, as you will find out, you have no internet connection using the VPN, you can fix that with [this link](https://ikdoeict.freshdesk.com/support/solutions/articles/31000137414-solution-ik-kan-niet-surfen-via-de-vpn).

## Base configuration (1.2)

Surf to [the cloud](https://cloud.ikdoeict.be/vcac) and make a new implementation of the course. Then fire them up and use VMRC to connect to the server (CentOS). Also the implementation will expire every 2 days, this is to force you to release all the resources, so everytime to work you will have to extend the lease of the implementation with 2 days. When expired you cannot start the machines.

The server has the a user with administrator rights named **student** with the password **Azerty123**. So log in and change the password ASAP using `sudo passwd student`.

The client has the same user and password, but that isnt as important to change in this excersize, as this is server focused, not client.

Also my machine did not have nano installed. As I am personally more familiar with nano, I installed it using `yum install nano`.

### Network configuration (1.3)

Firstly we need to get our networking in order, so on the server we simply type `sudo ip a` and take note of all internet adapters. As you can see below ours is **ens192**. The lo is simply a loopback.

![ip a result](images/IPa.PNG)

Alright, now that we know _what_ to change, let's do it! We will go to the file containing the basic network config and edit it. `sudo nano /etc/sysconfig/network-scripts/ifcfg-<adapter>`

The things you want to edit are:
```
ONBOOT=yes
BOOTPROTO=static
NM_CONTROLLED=no
IPADDR=<ip_server>
NETMASK=<subnet_server>
GATEWAY=<default_gateway>
```

Next up we are going to change the hostname, this is done simply with `set-hostname <name>`.

Afterwards go to `sudo nano /etc/resolv.conf` and add or edit the file to contain your wanted DNS's.
```
nameserver <dns>
```

Then, to finish up we are going to restart the service. This is done with `systemctl restart network`.
If everything is right you should be able to ping. This can be done by doing the following tests.
- `ping <default_gateway>` upon failure your gateway/mask is wrong.
- `ping 8.8.8.8` there is no connection to outside.
- `ping google.com` the DNS is wrong.
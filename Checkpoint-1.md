# Checkpoint 1

## Preperation

To start you will probably need a VPN connection to school. You can do that with [this link](https://ikdoeict.freshdesk.com/support/solutions/articles/31000136666-howto-verbinding-maken-naar-het-schoolnetwerk-via-vpn). Also, as you will find out, you have no internet connection using the VPN, you can fix that with [this link](https://ikdoeict.freshdesk.com/support/solutions/articles/31000137414-solution-ik-kan-niet-surfen-via-de-vpn).

## Base configuration (1.2)

Surf to [the cloud](https://cloud.ikdoeict.be/vcac) and make a new implementation of the course. Then fire them up and use VMRC to connect to the server (CentOS). Also the implementation will expire every 2 days, this is to force you to release all the resources, so everytime to work you will have to extend the lease of the implementation with 2 days. When expired you cannot start the machines.

The server has the a user with administrator rights named **student** with the password **Azerty123**. So log in and change the password ASAP using `sudo passwd student`.

The client has the same user and password, but that isnt as important to change in this excersize, as this is server focused, not client.

### Network configuration (1.3)

Firstly we need to get our networking in order, so on the server we simply type `sudo ip a` and take note of all internet adapters. As you can see below ours is **ens192**.

![ip a result](images/IPa.PNG)
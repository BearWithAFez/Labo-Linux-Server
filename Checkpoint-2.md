# Checkpoint 2

Everything in between angle brackets <> are meant to be filled in.
Also it might be a good idea to make a SNAPSHOT here. Incase something happens...

## DNS (1.4)

To start of we need to install Bind. To do this simply use `sudo yum install bind bind-utils` this will install both packages. This is the tool that will allow us to act as a DNS server ourselves. The 2 most used configuration files for the DNS are `sudo nano /etc/named.conf`, for the general settings of the NAME server, and `sudo nano /etc/resolv.conf`, for the configuration of the used DNS's.

As a first step let's set it up so that we can use ourselves as our own DNS server. We start of with editing our name configuration `sudo nano /etc/named.conf`

What we want is to only allow requests from inside OUR network (the allow query), that upon not finding it on our server we forward them to the other DNS's and that DNSsec is dissabled.

(DNS sec is a service to protect you from people altering the DNS records)

Under the options you want to edit/add the following lines: (the # is used to add comments)

```
#Listen-on port 53 {127.0.0.1; };
#listen-on-v6 port 53 { ::1; };
allow-query { 10.129.32.0/21; }; # Our network
forwarders { 10.129.28.232; 10.129.28.230; }; # forward DNS
forward only;	# Dont allow reverse DNS connection
dnssec-enable no;
dnssec-validation no;

```
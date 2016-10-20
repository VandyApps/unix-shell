## Networking Command Line Tools

### Introduction
In professional environments, you will probably be dealing with lots of virtual computers, and you will need to interact with them across a network via the command line. This session is an introduction into some helpful tools you can use in the command line environment to execute important networking processes and gather important networking information.

#### hostname
```
hostname
```

Tells the user the host name of the computer they are logged into. Note: may be called host.

#### host

Performs a simple lookup of an internet address (using the Domain Name System, DNS). Simply type:

```
host <ip_address>
```
or
```
host <domain_name>
```

#### dig

The "domain information groper" tool. More advanced than host... If you give a hostname as an argument to output information about that host, including it's IP address, hostname and various other information.

For example, to look up information about “www.amazon.com” type:
```
dig www.amazon.com
```
To find the host name for a given IP address (ie a reverse lookup), use dig with the `-x' option.
```
dig -x 100.42.30.95
```
This will look up the address (which may or may not exist) and returns the address of the host, for example if that was the address of “http://slashdot.org” then it would return “http://slashdot.org”.

dig takes a huge number of options (at the point of being too many), refer to the manual page for more information.

#### ifconfig

This command is used to configure network interfaces, or to display their current configuration. In addition to activating and deactivating interfaces with the “up” and “down” settings, this command is necessary for setting an interface's address information if you don't have the ifcfg script.

Use ifconfig as either:
```
ifconfig
```
This will simply list all information on all network devices currently up.
```
ifconfig eth0 down
```
This will take eth0 (assuming the device exists) down, it won't be able to receive or send anything until you put the device back “up” again.

Clearly there are a lot more options for this tool, you will need to read the manual/info page to learn more about them.

#### ping

The ping command (named after the sound of an active sonar system) sends echo requests to the host you specify on the command line, and lists the responses received their round trip time.

You simply use ping as:
```
ping <ip_or_host_name>
```
Note to stop ping (otherwise it goes forever) use CTRL-C (break)

#### traceroute

traceroute will show the route of a packet. It attempts to list the series of hosts through which your packets travel on their way to a given destination. Also have a look at xtraceroute (one of several graphical equivalents of this program).

Command syntax:
```
traceroute <machine_name_or_ip>
```
#### wget

(GNU Web get) used to download files from the World Wide Web.

To archive a single web-site, use the -m or --mirror (mirror) option.

Use the -nc (no clobber) option to stop wget from overwriting a file if you already have it.

Use the -c or --continue option to continue a file that was unfinished by wget or another program.

Simple usage example:
```
wget <url_for_file>
```
This would simply get a file from a site.

wget can also retrieve multiple files using standard wildcards, the same as the type used in bash, like *, [ ], ?. Simply use wget as per normal but use single quotation marks (' ') on the URL to prevent bash from expanding the wildcards. There are complications if you are retrieving from a http site (see below...).

Advanced usage example, (used from wget manual page):
```
wget --spider --force-html -i bookmarks.html
```
This will parse the file bookmarks.html and check that all the links exist.

Advanced usage: this is how you can download multiple files using http (using a wildcard...).

Notes: http doesn't support downloading using standard wildcards, ftp does so you may use wildcards with ftp and it will work fine. A work-around for this http limitation is shown below:
```
wget -r -l1 --no-parent -A.gif http://www.website.com[1]
```
This will download (recursively), to a depth of one, in other words in the current directory and not below that. This command will ignore references to the parent directory, and downloads anything that ends in “.gif”. If you wanted to download say, anything that ends with “.pdf” as well than add a -A.pdf before the website address. Simply change the website address and the type of file being downloaded to download something else. Note that doing -A.gif is the same as doing -A “*.gif” (double quotes only, single quotes will not work).

wget has many more options refer to the examples section of the manual page, this tool is very well documented.

Alternative website downloaders: You may like to try alternatives like httrack. A full GUI website downloader written in python and available for GNU/Linux

#### curl

curl is another remote downloader. This remote downloader is designed to work without user interaction and supports a variety of protocols, can upload/download and has a large number of tricks/work-arounds for various things. It can access dictionary servers (dict), ldap servers, ftp, http, gopher, see the manual page for full details.

One thing that curl is great for is simple HTML inspection:
```
curl vandyapps.club
```
will return the raw HTML of the vandyapps.club webpage right to your command line. This is helpful for a variety of web development uses.

To access the full manual (which is huge) for this command type:
```
curl -M
```
For general usage you can use it like wget. You can also login using a user name by using the -u option and typing your username and password like this:
```
curl -u username:password http://www.placetodownload/file
```
To upload using ftp you the -T option:
```
curl -T file_name ftp://ftp.uploadsite.com
```
To continue a file use the -C option:
```
curl -C - -o file http://www.site.com
```

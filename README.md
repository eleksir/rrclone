# RPM Repositories Cloning tool

1 to 1 rpm repository cloning tool

## Getting Started

rrclone http://source/repo/ /absolute/path/to/destination/folder/

### Prerequisites

Linux or FreeBSD with recent perl (at least 5.20, on previous versions i didn't
test it). There is no external packages required in order to run this program.
The only thing that required is Perl. But many linux distributions have
ill-minded practice to rip Perl into many sub-packages, in this case you have
to install some perl packages.

for ubuntu: libjson-pp-perl, libfile-spec-perl, libxml-parser-perl,
libio-compress-perl, liburi-perl

in case of Slackware Linux everything is already shipped with single Perl
package.

```
# apt install libjson-pp-perl libfile-spec-perl libxml-parser-perl \
libio-compress-perl liburi-perl
```

A correct path to repository. You need a string after "baseurl=" in repo-file
(one that located in /etc/yum.repos.d, for example), it must end with trailng
slash. If it does not, just add it.

To check that url is correct you can try to download part of repository xml
metadata. Put your string into browser address bar and add
"repodata/repomd.xml" (no quotes) and if you see xml text then - vua-la! -
your string is correct.

### Installing

There are no additional effort required for one-shot sync.

But if you planning to keep repository in sync with upstream, you should add
cron job, that can be run without any additional privileges, i.e. web server
user is enough for that.

to add cronjob invoke

```
su -s /bin/bash apache
crontab -e
```

```
30 4 * * 0 /path/to/rrclone http://repository/url/ /absolute/path/to/copy/
```

This will run job weekly, at Sunday 4:30.

## Deployment

Obviously, before deploy this script on some production environment you should
package it properly :) 

## Contributing

If you want contribute ideas or code - please feel free to contact me via
email eleksir at exs-elm.ru

## Authors

* **Eleksir** - *Initial work* - [exs' corner](https://exs-elm.ru/hg/rrclone)

## License

This project is licensed under the BSD License - see the [LICENSE](LICENSE) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* you

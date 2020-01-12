# RPM Repositories Cloning tool

1 to 1 rpm repository cloning tool

## Getting Started

```bash
rrclone http://source/repo/ /absolute/path/to/destination/folder/
```

### Prerequisites

Linux or FreeBSD with recent perl (at least 5.20, on previous versions i didn't
test it). Perl modules required: AnyEvent, AnyEvent::HTTP, JSON::PP,
XML::Parser, URI::URL

#### For ubuntu it is enough to perform

```bash
sudo apt install libjson-pp-perl libfile-spec-perl libxml-parser-perl \
liburi-perl libanyevent-http-perl
```

#### For centos 7+ it is enough to perform

```bash
yum install perl-AnyEvent-HTTP perl-JSON-PP perl-XML-Parser perl-URI \
perl-IO-Zlib
```

#### Cpanminus way

There is a way to install all modules locally either to application dir or to
user profile. All you need in this case is cpanminus. Some **perl-App-cpanm**
or cpm or carton or so. In most bad case you can wget it from cpanminus
[github](https://github.com/miyagawa/cpanminus/raw/devel/App-cpanminus/cpanm)
directly.

Also you'll need analogue of centos **@development** metapackage (package group
Development Tools) or Ubuntu **build-essential** metapackage to build perl'
binary modules.

To prepare environment you need to run **./bootstrap.sh** in rrclone directory.
**Never run it as root**, or packages will be installed directly in system.

In case of package, providing perl' **local::lib** found in system dependencies
will be installed in script directory in **vendor_perl** catalogue, else it will
go to **~./perl5**.

To run script properly you should setup environment variables pointing to these
vendored modules.

```bash
export PERL5LIB="/path/to/rrclone/dir/vendor_perl/lib/perl5"
```

and in case if perl' local::lib is not found in system:

```bash
export PERL5LIB="$HOME/.perl5/lib/perl5"
```

### Using rrclone

There are no additional effort required for one-shot sync.

You need correct path to repository. A string after "baseurl=" in repo-file
(one that located in **/etc/yum.repos.d**, for example), it must end with
**trailng slash**. If it does not, just add it.

To check that url is correct you can try to download part of repository xml
metadata. Put your string into browser address bar and add
"repodata/repomd.xml" (no quotes) and if you see xml text then - vua-la! -
your string is correct.

But if you planning to keep repository in sync with upstream, you should add
cron job, that can be run without any additional privileges, i.e. web server
user is enough for that.

To add cronjob invoke

```bash
su -s /bin/bash apache
crontab -e
```

```text
30 4 * * 0 /path/to/rrclone http://repository/url/ /absolute/path/to/copy/
```

This will run job weekly, at Sunday 4:30.

## Deployment

Obviously, before deploy this script on some production environment you should
package it properly :)

And as a good practice do not run it as root user.

## Contributing

If you want contribute ideas or code - please feel free to contact me via
email eleksir at exs-elm.ru

## Authors

* **Eleksir** - *Initial work* - [exs' bitbucket](https://bitbucket.org/eleksir/rrclone/src/master/)

## License

This project is licensed under the BSD License - see the [LICENSE](LICENSE) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* you

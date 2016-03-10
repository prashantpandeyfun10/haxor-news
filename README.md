![Imgur](http://i.imgur.com/SLw1Cc6.gif)

haxor-news
=================

View and filter Hacker News posts, comments, and linked web content without leaving the command line.  Comes with auto-completion and interactive help.

> *Coworker who sees me looking at something in a browser: "Glad you're not busy; I need you to do this, this, this..."*
>
> *Coworker who sees me staring intently at a command prompt: Backs away, slowly...*
>
> *-[Source](https://www.reddit.com/user/foxingworth)*

Spend a lot of time on the terminal?  Spend a lot of time on Hacker News?

`haxor-news` brings Hacker News to the terminal, allowing you to view and filter linked web pages and comments without leaving your command line.

* Want to expand only previously unseen comments?
    * `-cu/--comments_unseen`
* How about comments recently posted in the past 60 minutes?
    * `-cr/--comments_recent`
* Filter comments with a regex query?
    * `-cq/--comments_query [query]`

Need help remembering these options?

![Imgur](http://i.imgur.com/MuUO5wW.png)

Job hunting or just curious what's out there?  Filter the monthly who's hiring or freelancers post:

    $ hn hiring "(?i)(Node|JavaScript).*(remote)" > remote_web_jobs.txt

Combine `haxor-news` with pipes, redirects, and other command line utilities: Output to pagers, write to files, automate with cron, etc.

![Imgur](http://i.imgur.com/F08ywcD.png)

## Index

### General

* [Syntax](#syntax)
* [Auto-Completer and Interactive Help (Optional)](#auto-completer-and-interactive-help-optional)
* [Commands](#commands)


### Features

* [View Posts](#view-posts)
* [View a Post's Linked Web Content](#view-a-posts-linked-web-content)
* [View and Filter a Post's Comments](#view-and-filter-a-posts-comments)
    * [View All Comments](#view-all-comments)
    * [Filter on Unseen Comments](#filter-on-unseen-comments)
    * [Filter on Recent Comments](#filter-on-recent-comments)
    * [Filter with Regex](#filter-with-regex)
* [View and Filter the Monthly Hiring Post](#filter-the-monthly-hiring-post)
* [View and Filter the Monthly Freelancer Post](#filter-the-monthly-hiring-post)
* [Combine With Pipes and Redirects](#combine-with-pipes-and-redirects)
* [View User Info](#view-user-info)
* [View Onions](#view-onions)
* [View in a Browser](#viewing-results-in-a-browser)
* [TODO](#todo)
    * [Submit Posts and Comments](#todo)
    * [Search Posts and Comments](#todo)
    * [Customize Color Scheme](#todo)

### Installation and Tests

* [Installation](#installation)
    * [Pip Installation](#pip-installation)
    * [Virtual Environment Installation](#virtual-environment-installation)
    * [Supported Python Versions](#supported-python-versions)
    * [Supported Platforms](#supported-platforms)
* [Developer Installation](#developer-installation)
    * [Continuous Integration](#continuous-integration)
    * [Unit Tests and Code Coverage](#unit-tests-and-code-coverage)
    * [Documentation](#documentation)

### Misc

* [Contributing](#contributing)
* [Credits](#credits)
* [Contact Info](#contact-info)
* [License](#license)

## Syntax

Usage:

    $ hn <command> [params] [options]

## Auto-Completer and Interactive Help (Optional)

Optionally, you can enable fish-style completions plus an auto-completion menu with interactive help:

    $ haxor-news

Within the auto-completer, the same syntax applies:

    haxor> hn <command> [params] [options]

![Imgur](http://i.imgur.com/L2rzgb3.png)
![Imgur](http://i.imgur.com/FL2pyC0.png)

## Commands

![Imgur](http://i.imgur.com/oqvUbj8.png)

## View Posts

View Top, Best, Show, Show, Ask, Jobs, New, and Onion posts.

Usage:

    $ hn [command] [limit]  # post limit default: 10

Examples:

    $ hn top
    $ hn show 30 | less

![Imgur](http://i.imgur.com/6kZG84S.png)

## View a Post's Linked Web Content

After viewing a list of posts, you can view a post's linked web content by referencing the post `#`.

The HTML contents of the post's link are **formatted for easy-viewing within your terminal**.  If available, the formatted output is sent to a pager.

See the [View in a Browser](#viewing-results-in-a-browser) section to view the contents in a browser instead.

Usage:

    $ hn view [#]

Example:

    $ hn view 1
    $ hn view 8

![Imgur](http://i.imgur.com/yWKASiQ.png)

## View and Filter a Post's Comments

### View All Comments

After viewing a list of posts, you can view a post's comments by referencing the post `#`.

Examples:

    $ hn view 8 -c
    $ hn view 8 --comments > comments.txt

![Imgur](http://i.imgur.com/fcBUnim.png)

### Filter on Unseen Comments

Filter comments to expand only those you have not yet seen.  Unseen comments are denoted with a `[!]` and are fully expanded.

Seen comments will be truncated with [...] and will be shown to help provide context to unseen comments.

Examples:

    $ hn view 8 -cu
    $ hn view 8 --comments_unseen | less

![Imgur](http://i.imgur.com/mR4uKY0.png)

### Filter on Recent Comments

Filter comments to expand only those **posted within the past 60 minutes**.

Older comments will be truncated with [...] and will be shown to help provide context to recent comments.

Examples:

    $ hn view 8 -cr
    $ hn view 8 --comments_recent

![Imgur](http://i.imgur.com/LfquzlG.png)

### Filter with Regex

Filter comments based on a given regular expression query.

Example:

    $ hn view 2 -cq "(?i)programmer"
    $ hn view 2 --comments_regex_query "(?i)programmer" > programmer.txt

*Case insensitive regex: `(?i)`*

![Imgur](http://i.imgur.com/1IpPwZF.png)

## Filter the Monthly Hiring Post

Hacker News hosts a monthly hiring post where employers post the latest job openings.

Usage:

    $ hn hiring [regex filter]

Examples:

    $ hn hiring ""
    $ hn hiring "(?i)JavaScript|Node"
    $ hn hiring "(?i)(Node|JavaScript).*(remote)" > remote_jobs.txt

*Case insensitive regex: `(?i)`*

![Imgur](http://i.imgur.com/Lwz8iwG.png)

To search a different monthly hiring post other than the latest, use the hiring post id.

Usage:

    $ hn hiring [regex filter] [post id]

## Filter the Freelancers Post

Hacker News hosts a monthly freelancers post where employers and freelancers post availabilities.

Usage:

    $ hn freelancer [regex filter]

Examples:

    $ hn freelancer ""
    $ hn freelancer "(?i)JavaScript|Node"
    $ hn freelancer "(?i)(Node|JavaScript).*(remote)" > remote_jobs.txt

*Case insensitive regex: `(?i)`*

![Imgur](http://i.imgur.com/TnBDFGk.png)

To search a different monthly hiring post other than the latest, use the hiring post id.

Usage:

    $ hn freelancer [regex filter] [post id]

## Combine With Pipes and Redirects

Output to pagers, write to files, automate with cron, etc.

Examples:

    $ hn view 1 -c | less
    $ hn freelancer "(?i)(Node|JavaScript).*(remote)" > remote_jobs.txt

![Imgur](http://i.imgur.com/x2aj7SM.png)

## View User Info

Usage:

    $ hn user [user id]

![Imgur](http://i.imgur.com/d8VpmmQ.png)

## View Onions

Usage:

    $ hn onion [limit]  # post limit default: all

![Imgur](http://i.imgur.com/ZdXQXWY.png)

## View in a Browser

View the linked web content or comments in your default browser instead of your terminal.

Usage:

    $ hn <command> [params] [options] -b
    $ hn <command> [params] [options] --browser

## TODO

* Submit posts and comments
* Search posts and comments
* Customize color scheme

## Installation

### Pip Installation

[![PyPI version](https://badge.fury.io/py/saws.svg)](http://badge.fury.io/py/saws) [![PyPI](https://img.shields.io/pypi/pyversions/saws.svg)](https://pypi.python.org/pypi/saws/)

`hncli` is hosted on [PyPI](https://pypi.python.org/pypi/hncli).  The following command will install `hncli`:

    $ pip install hncli

You can also install the latest `hncli` from GitHub source which can contain changes not yet pushed to PyPI:

    $ pip install git+https://github.com/donnemartin/hacker-news-cli.git

If you are not installing in a virtualenv, run with `sudo`:

    $ sudo pip install hncli

Once installed, run `hncli`:

    $ hn [command] [options]

### Supported Python Versions

* Python 2.6
* Python 2.7
* Python 3.3
* Python 3.4
* Python 3.5

### Supported Platforms

* Mac OS X
    * Tested on OS X 10.10
* Linux, Unix
    * Tested on Ubuntu 14.04 LTS
* Windows
    * Tested on Windows 7 and 10

### Documentation

[![Documentation Status](https://readthedocs.org/projects/saws/badge/?version=latest)](http://saws.readthedocs.org/en/latest/?badge=latest)

Source code documentation is available on [Readthedocs.org](http://saws.readthedocs.org/en/latest/?badge=latest).

Run the following to build the docs:

    $ scripts/update_docs.sh

## Contributing

Contributions are welcome!

Review the [Contributing Guidelines](https://github.com/donnemartin/haxor-news/blob/master/CONTRIBUTING.md) for details on how to:

* Submit issues
* Submit pull requests

## Credits

* [click](https://github.com/mitsuhiko/click) by [mitsuhiko](https://github.com/mitsuhiko)
* [haxor](https://github.com/avinassh/haxor) by [avinassh](https://github.com/avinassh)
* [html2text](https://github.com/aaronsw/html2text) by [aaronsw](https://github.com/aaronsw)
* [python-prompt-toolkit](https://github.com/jonathanslenders/python-prompt-toolkit) by [jonathanslenders](https://github.com/jonathanslenders)
* [requests](https://github.com/kennethreitz/requests) by [kennethreitz](https://github.com/kennethreitz)

## Contact Info

Feel free to contact me to discuss any issues, questions, or comments.

My contact info can be found on my [GitHub page](https://github.com/donnemartin).

## License

[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

    Copyright 2015 Donne Martin

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

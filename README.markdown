rerun
=====

`rerun` is a tiny little script that helps you run repetetive shell commands
over and over again.

The Problem
-----------

Imagine you're working on debugging an issue with a particular daemon, like
Celery.  In one window you're editing code to try solutions, and in another
you're stopping and starting the Celery and RabbitMQ daemons.

The commands
you're running over and over in varying order might look like this:

    sudo /etc/init.d/rabbitmq-server restart
    sudo /etc/init.d/celeryd stop
    sudo /etc/init.d/celeryd start
    tail /var/log/celery/myhost.log
    tail /var/log/celery/myotherhost.log

Running the various commands can be a pain.  They're similar enough that tab
completion, zsh's history completion, and `Ctrl-R` searching all fall short.
That's where `rerun` comes in:

![Screenshot of a rerun session](http://i.imgur.com/QcsuD.png)

Installation
------------

    curl 'http://bitbucket.org/sjl/src/tip/rerun' > /usr/local/bin/rerun
    chmod a+x /usr/local/bin/rerun

Usage
-----

When you run `rerun` you're greeted with a prompt like this:

    >

Type /help (or just /h) to get a list of commands:

    > /help
    (/a)dd [command]
    (/d)elete [key]
    (/h)elp
    (/q)uit

    > 

Add commands to the list with /add.  You can specify the command right in the
/add command or let `rerun` prompt you for it:

    > /add ls

    [a] ls
    > /add
    Enter command: pwd

    [a] ls
    [b] pwd
    > 

Now that you've got some commands in the list, run them by entering the key
displayed next to their name:

    [a] ls
    [b] pwd
    > a
    LICENSE.markdown	README.markdown		rerun

    [a] ls
    [b] pwd
    > b
    /Users/sjl/src/rerun

    [a] ls
    [b] pwd
    > 

If you don't need a command any more you can /delete it:

    [a] ls
    [b] pwd
    > /delete b

    [a] ls
    > /d
    Which command? a

    > 

Use /quit or `Ctrl-D` to exit.

Other Information
-----------------

* Source (Mercurial): <http://bitbucket.org/sjl/rerun/>
* Source (Git): <http://github.com/sjl/rerun/>
* License: MIT/X11
* Issues: <http://github.com/sjl/rerun/issues/>

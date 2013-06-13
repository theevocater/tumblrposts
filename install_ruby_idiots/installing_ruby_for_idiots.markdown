# Installing Ruby For Idiots (like me)

I've previously had some trouble installing ruby because so I've endeavored to
create a guide that even I could use to successfully install ruby. This guide
assumes that you have a basic understandings of a shell (something along the
lines of "I know how to open a terminal on my computer"). Hopefully you can get
by just pasting each command in to your shell and then reading the output.
[[MORE]]
Some quick basics: lines starting with <code>$</code> are things to be
entered at the shell. If something <code>looks like code</code> but doesn't
start with $ its either the output of a command or something to put into
a file.

## Install

If you ever run in to trouble or things aren't working, please consult the
troubleshooting section.

### Installing ruby-build

The first thing you are going to want is
[ruby-build](https://github.com/sstephenson/ruby-build). This small shell
script will allow you to install various versions of ruby.

    $ git clone git://github.com/sstephenson/ruby-build.git
    $ cd ruby-build/
    $ sudo ./install.sh

Super simple and it installs everything in /usr/local. If you would rather
install it somewhere else just run the following *before* running ./install.sh

    $ export $PREFIX="/where/you/want"

#### Install some rubies

Now that we have ruby-build, let us install a ruby.

    $ ruby-build --definitions

That gives us a list of all the rubies ruby-build knows about. I happened to need
ruby 1.9.2 so let's install that and the latest ruby-2.

The first argument is just the version you want as it appears exactly in the
--definitions list. The second argument is the dir to install ruby in. chruby
recommends you install things at /opt/rubies but I like to keep things in my
homedir on my laptop. Where you install ruby isn't super important, chruby just
has to know where they are. 

_Tip_: chruby can understand some short hand if you follow the pattern of
rubytype-version-patchlevel in your install directory like I do.

    $ ruby-build 1.9.2-p320 ~/.rubies/ruby-1.9.2-p320
    $ ruby-build 2.0.0-p195 ~/.rubies/ruby-2.0.0-p195
    $ ruby-build $more_rubies $more_places

### Install chruby

Okay, now that you (hopefully) have some rubies installed, let's go over
changing between them. We are going to install
[chruby](https://github.com/postmodern/chruby). Luckily its a really simple
script, just like ruby-build.

    $ wget -O chruby-0.3.5.tar.gz https://github.com/postmodern/chruby/archive/v0.3.5.tar.gz
    $ tar -xzvf chruby-0.3.5.tar.gz
    $ cd chruby-0.3.5/
    $ sudo make install

Almost done! Just need to add some lines to your shell configuration
for chruby.

    if [[ -s "/usr/local/share/chruby/chruby.sh" ]] ; then
      # this line adds all the helpful chruby stuff to your environment
      source /usr/local/share/chruby/chruby.sh
      # this line defines a bash array of your rubies
      # you could also do something like RUBIES=("/some/places", "something/else/")
      # the * just grabs all rubies installed in that directory
      export RUBIES=("$HOME/.rubies/*")
      # or if you went with /opt/rubies:
      # export RUBIES=("/opt/rubies/*")
    fi

Save that to ~/.bash_profile (or whatever is appropriate) and reopen your shell!

### Using chruby

Now for the easiest part: using chruby.

    $ chruby 1.9.2

or 

    $ chruby ruby-1.9.2-p320

If you followed my lead and installed ruby-1.9.2-p320 you should now be using
it. We can check by running

    $ ruby --version
    ruby 1.9.2p320 (2012-04-20 revision 35421) [i686-linux]

You should see the same (or at least similar to the version you installed).

Chruby is also helpful because it sets up the correct environment as well:

    $ export
    declare -x GEM_HOME="/home/jdkaufma/.gem/ruby/1.9.2"
    declare -x GEM_PATH="/home/jdkaufma/.gem/ruby/1.9.2:/home/jdkaufma/.rubies/ruby-1.9.2-p320/lib/ruby/gems/1.9.1"
    declare -x GEM_ROOT="/home/jdkaufma/.rubies/ruby-1.9.2-p320/lib/ruby/gems/1.9.1"
    declare -x RUBYOPT=""
    declare -x RUBY_ENGINE="ruby"
    declare -x RUBY_ROOT="/home/jdkaufma/.rubies/ruby-1.9.2-p320"
    declare -x RUBY_VERSION="1.9.2"

When run as a user it will direct gems to be installed locally and sets up the
correct flags for ruby.

### (Optional) Bundler

If you are new to ruby like me, you will probably also want to install bundler.
Bundler is a simple ruby gem that helps install other gems. In your ruby
project you list some depencies and bundler knows how to install them all. To
install bundler (and any other gem) we use the program aptly named "gem".

    gem install bundler

## Troubleshooting

#### OSX: unable to build rubies older than 1.9.3-p125

Here you will need the excellent [homebrew](http://mxcl.github.io/homebrew/)
which you will want regardless.  Follow their instructions for installing
homebrew and then run the command ruby-build printed out. If you lost it:

     $ brew tap homebrew/dupes && brew install apple-gcc42

Now rerun your ruby-build.

## Closing

After all that you should now have a basic system for installing and using
ruby. If you run into any trouble or have amendments to this document, please
feel free to find me on twitter @theevocater. I also accept pull requests at
[github](https://github.com/theevocater/tumblrposts/blob/master/install_ruby_idiots/installing_ruby_for_idiots.markdown).

## Helpful links

* [ruby-build github](https://github.com/sstephenson/ruby-build)
* [chruby github](https://github.com/postmodern/chruby)
* [bundler site](http://gembundler.com/)
* [Steve's post that inspired this article](http://blog.steveklabnik.com/posts/2012-12-13-getting-started-with-chruby)

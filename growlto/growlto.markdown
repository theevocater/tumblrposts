I wanted to have growl and decided it wouldn't be too hard to just build it
myself. There were some snags so I've made a simple howto.
<p>[[MORE]]</p>
## Steps:

  1. Install Xcode (Download from appstore)
  2. Install hg, svn, git (I _think_ osx ships with most of these)
  3. `hg clone <https://code.google.com/p/growl/>`
  4. `cd growl`
  5. `hg update "Growl.app 2.0.1"` (or current, check `hg tags`)
  6. click Growl.xcodeproj
  7. Make sure you are building Growl.app
  8. click run button.
  9. if it runs, celebrate! and close Growl (if not see below)
  10. go to build products in Xcode, show in finder. ![Visual to find build products](http://media.tumblr.com/f96d0d956893b3ccc7ac8a5dcbbc26e4/tumblr_inline_mh7ip2ix721qhzxqy.png)
  11. copy growl.app to /Applications and great success!

### Fails to build?

  1. close Xcode
  2. Open Keychain Access.app
  3. Click Keychain Access Menu -> Certificate Assistant -> Create Certificate ![Create Cert Menu](http://media.tumblr.com/f2e3add3a0acb037c3c28a0bed6c3781/tumblr_inline_mh7k53Myrn1qhzxqy.png)
  4. use "3rd Party Mac Developer Application: The Growl Project, LLC" as cert name ![Create Certificate Screen](http://media.tumblr.com/f27bcab6f92cd656429050fb6cd88930/tumblr_inline_mh7k5twHsQ1qhzxqy.png)
  5. reopen Growl.xcodeproj
  6. try building again

sourced from with some pain from <http://growl.info/documentation/developer
/growl-source-install.php>


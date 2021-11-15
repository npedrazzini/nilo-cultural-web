---
layout: post
title: Troubleshooting of common Terminal issues
---
1. > `bash: jekyll: command not found`

    Why: you have not set your RubyGems PATH correctly when you installed Ruby.
    At least these paths should be in your $PATH variable: 
    - /usr/local/bin
    - /usr/bin
    - /bin
    - /usr/local/opt/ruby/bin
    - /usr/local/lib/ruby/gems/3.0.0/bin
    When your run `echo $PATH` they should appear in this order:

    `/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:/usr/local/bin:/usr/bin`

    Note that each PATH is separated by a colon : and the order matters! If you played around with other package or added other PATHs to the above, yours might look a bit different, but as long as the relative order between the PATHs indicated above is respected that should be OK.

    How to fix the PATH if it's messed up. 
    Run:
    `open ~/.bash_profile`
    This should open the file .bash_profile in a text editor. It didn't? Well, then you probably messed up more than you thought. If running this command does nothing, then your .bash_profile is probably only corrupted (i.e. it contains lines that are badly written). You have to open it manually:

    - On the top bar in your Mac, go to **Go > Computer > Macintosh HD > Users > yourusername**. 
    - Press **Command + Shift + .** (dot/full stop) to show hidden files.
    - Open .bash_profile

    If by running `open ~/.bash_profile` you get an error saying the file doesn't exist, then you messed up worse than you thought. You probably deleted the file by mistake. Create a new one by running:
    `touch ~/.bash_profile`
    Then open it.

    Once you opened your .bash_profile, add the following two lines to the bottom of the file, in this order:

    `export PATH="/usr/local/bin:/usr/bin:/bin:$PATH"`

    `export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"`

    Note: this is the same (just the manual way) as running:

    `echo 'export PATH="/usr/local/bin:/usr/bin:/bin:$PATH"' >> ~/.bash_profile`

    `echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.bash_profile`


2. > Old blog posts showed correctly, new ones don't.

    Why: you probably did not name the blog post file correctly. The name format of a Jekyll blog post is very rigid. It needs to start with a date and have the following shape:

    **YYYY-MM-DD-yourtitle.md**

    Where YYYY is the year, MM the month and DD the day. No other format allowed.

3. > I've tested the blog locally using jekyll serve and it worked, then I pushed it to GitHub and the website did not update. 

    Well, chances are that you just have to WAIT! It takes time, up to a few hours sometimes.

4. > You haven't tested your blog before pushing it and your GitHub page doesn't show/has a weird layout/etc.

    Well... you should have tested it before. That's the easiest way to find out where you went wrong. By running 
    `jekyll serve` you get messages about what the problem is. For example: you added characters to the YAML frontmatter that are not allowed.

5. > When you run `jekyll serve` you get an error about `webrick` not being installed. 

    Just run: 

    `bundle add webrick`
    
    `bundle install`

    Try `jekyll serve` again. If you still get an error, try serving jekyll via bundler: 

    `bundle exec jekyll serve`

    And if this works it probably means that for some reason you are running jekyll on a different Ruby version than the one required by your jekyll website. Keep using `bundle exec jekyll serve` from now on and contact me directly to solve the issue. 
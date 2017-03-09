# Simple Demo for Git Bisect

This git repository has only one purpose: It has a relatively
long history with one harmful commit in there.

From this commit on, a script and a Java unit test start
failing (that is, the script exits with status 1 and 
the unit test has an assertion error).

Just imagine, that all the commits between the tag _base_ and
the head of the _master_ branchis the work of your day and
you have not noticed these errors until, near the end of this
day, you start the maven build and you see, that this is not
working any more.

Without having git, you would now go deep into all of your changes
you have done this day and would - maybe by just staring
sense into the failures - try to find out what and (most
importantly) when things turned out to go the wrong way.

But now you have git! You haven't heard about git bisect?
Now it's definitely the right time to change this.

All you have to do is

1. Go to the head of the master branch (if you aren't here
already)
1. Start git bisect, telling git that the current commit is bad:

   `git bisect bad`
   
   (Yes git, please start bisect for me)
1. Checkout the last commit you know that was good:

   `checkout base`
   
   `git bisect good`
1. Let git search for the foul commit, either
   * by executing commands and telling git whether the current commit
     is good or bad:
    
     `git bisect good|bad`
    
     Using this, you only would have to check some commits by hand
     until git tells you, that it has found the foul commit.
   * or by telling git to execute a command that tells it whether the
     commit is good or bad:
    
     `git bisect run mvn test`
    
     Now all you have to do is wait, until git tells you the result.
1. When you're done, just stop the machinery:

   `git bisect reset`

Belief me, when you have seen this little magic, you will reconsider
squashing commits.

**Have fun!**

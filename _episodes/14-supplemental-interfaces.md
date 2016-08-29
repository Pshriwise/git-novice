---
title: Using Git from a text editor
teaching: 10
exercises: 0
questions:
- "Can I use Git with my text editor?"
objectives:
- "Understand that there are convenient ways to use Git other than the command-line."
- "Using non-command-line Git interfaces is useful but only after having a solid understanding of command-line Git."
keypoints:
- "See Git in action outside of the command-line."
---

Up until now, we've used Git commands within the shell to interact with a Git repository.
It is possible to use Git in other ways.  Many modern text editors like Sublime Text, Adobe Brackets,
or Microsoft Code have nice capabilities for using Git.  GitHub.com even produces its own popular
text editor called Atom, which naturally has Git integrated.  Integrated Development Environments (IDEs) like 
RStudio, Eclipse, or Apple's XCode are also able to use Git, if not natively, with a plugin/extension.

The main problem with using Git through a non-shell interface is that the mechanics of using Git are
less explicit than they are with the shell.  Furthermore, usually the integrations that are seen are
not comprehensive:  the most common Git operations are available from the application, but more
esoteric operations need to be done from the shell.  That is why it is important to view application
Git integration as a way to **assist, not replace** using Git.  

Here is an example of using a text editor that integrates Git.  We'll switch back and forth using the 
shell and the application (in this case Microsoft VS Code).

~~~
$ mkdir fruit
$ cd fruit/
$ git init
~~~
{: .bash}
~~~
Initialized empty Git repository in /Users/Me/Desktop/data-shell/fruit/.git/
~~~
{: .output}
~~~
$ code .
~~~
{: .bash}
 
The "`code .`" command opens the "`.`" directory, which happens to be "`fruit`" because we used "`cd`" to
get there.

<script src="{{ site.github.url | replace_first: 'http:', 'https:' }}/assets/js/better-simple-slideshow.min.js"></script>
<div class="bss-slides">
        <figure>
            <img src="/fig/vscode-1-1.png" width="100%" />
            <figcaption>Fig 1.1: Make a new file and call it "list.txt"</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-1-2.png" width="100%" />
            <figcaption>Fig 1.2: A (1) notification appears above the Git icon on the left.</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-1-3.png" width="100%" />
            <figcaption>Fig 1.3: Clicking on the Git pane, we can see there is a new file listed under the changes.</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-1-4.png" width="100%" />
            <figcaption>Fig 1.4: Going back to the files pane, and adding some text to the file.</figcaption> 
        </figure>
</div>

We now have a file called "`list.txt`" in the "`fruit`" directory, and we've saved it.  Let's go back to
the shell and see what our "`fruit`" directory looks like and what Git's status is:    

~~~
$ ls
~~~
{: .bash}
~~~
list.txt
~~~
{: .output}
~~~
$ git status
~~~
{: .bash}
~~~
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	list.txt

nothing added to commit but untracked files present (use "git add" to track)
~~~
{: .output}

Now let's add and commit this new file with Git:

~~~
$ git add list.txt
$ git commit -m "An initial list of fruit."
~~~
{: .bash}
~~~
[master (root-commit) d496271] An initial list of fruit.
 1 file changed, 4 insertions(+)
 create mode 100644 list.txt
~~~
{: .output}

At this point, a curious thing has happened inside of VS Code.  The "(1)" notification over the Git icon
on the left is now missing, meaning the our fruit Git repository is up to date. Let's now edit the
"`list.txt`" file, save, see what happens, then do a "`git add`", and a "`git commit -m`" from VS Code:

<div class="bss-slides">
        <figure>
            <img src="/fig/vscode-2-1.png" width="100%" />
            <figcaption>Fig 2.1: The (1) notification above the Git pane is gone.</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-2-2.png" width="100%" />
            <figcaption>Fig 2.2: We add the "tomatoes" line to the file and save the file.  Now the (1) notification is back.</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-2-3.png" width="100%" />
            <figcaption>Fig 2.3: Click on the Github pane, click on the file, then hovering the mouse over the file, a "+" will appear.  This does a "stage", just like "git add"</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-2-4.png" width="100%" />
            <figcaption>Fig 2.4: Now the file is staged and we want to commit, we'll add a message in the box above.</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-2-5.png" width="100%" />
            <figcaption>Fig 2.5: Click the checkmark above the message box to do a "git commit"</figcaption> 
        </figure>
        <figure>
            <img src="/fig/vscode-2-6.png" width="100%" />
            <figcaption>Fig 2.6: The file is committed and the repository is up to date.</figcaption> 
        </figure>
</div>

And now let's go back to the shell, check the git status, and see if our log reflects the changes:

~~~
$ git status
~~~
{: .bash}
~~~
On branch master
nothing to commit, working directory clean
~~~
{: .output}
~~~
$ git log
~~~
{: .bash}
~~~
commit a6b1c32df3dcde665a0513bba60706c4d4231c6a
Author: Me <me@wisc.edu>
Date:   Fri Aug 26 10:42:43 2016 -0500

    Added tomatoes to list.

commit d49627112de703f7dcc55c4169ee790cc038374a
Author: Me <me@wisc.edu>
Date:   Fri Aug 26 10:26:12 2016 -0500

    An initial list of fruit.
~~~
{: .output}

### Git operations on Github.com

On Github it's quick to find a history of Git commits, and it's easy to see changes in files.  But it's
also possible to also edit files and commit changes directly on the GitHub website.  This is useful
sometimes for things like typos or edits to documentation (the non-code parts of software).  But
editing code on the Github website is not ideal because, as much as possible, editing code should be 
done in the same environment as running/testing/debugging that code.  On the github website, you don't
have this possibility.

<script>
       var opts = { auto : false };
       makeBSS('.bss-slides', opts);
</script>

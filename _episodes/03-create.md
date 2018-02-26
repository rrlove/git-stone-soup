---
title: Creating a Repository
teaching: 10
exercises: 0
questions:
- "Where does Git store information?"
objectives:
- "Create a local Git repository."
keypoints:
- "`git init` initializes a repository."
---

Once Git is configured,
we can start using it.
Let's create a directory for our work and then move into that directory:

~~~
$ mkdir stonesoup
$ cd stonesoup
~~~
{: .bash}

Then we tell Git to make `stonesoup` a [repository]({{ page.root }}/reference/#repository)—a place where
Git can store versions of our files:

~~~
$ git init
~~~
{: .bash}

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~
$ ls
~~~
{: .bash}

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `stonesoup` called `.git`:

~~~
$ ls -a
~~~
{: .bash}

~~~
.	..	.git
~~~
{: .output}

Git stores information about the project in this special sub-directory.
If we ever delete it,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .bash}

~~~
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

> ## Places to Create Git Repositories
>
> We start a new project, `different_versions`, related to our `stonesoup` project.
> We enter the following sequence of commands to
> create one Git repository inside another:
>
> ~~~
> $ cd                      # return to home directory
> $ mkdir stonesoup              # make a new directory guac
> $ cd stonesoup                 # go into stonesoup
> $ git init                # make the stonesoup directory a Git repository
> $ mkdir different_versions    # make a sub-directory guac/different_versions
> $ cd different_versions       # go into stonesoup/different_versions
> $ git init                # make the different_versions sub-directory a Git repository
> ~~~
> {: .bash}
>
> Why is it a bad idea to do this? (Notice here that the `stonesoup` project is now also tracking the entire `different_versions` repository.)
> How can we undo our last `git init`?
>
> > ## Solution
> >
> > Git repositories can interfere with each other if they are "nested" in the
> > directory of another: the outer repository will try to version-control 
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown 
> > above:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> >
> > Note that we can track files in directories within a Git:
> >
> > ~~~
> > $ touch axe nail button                              # create files for variants of this story
> > $ cd ..                                         # return to stonesoup directory
> > $ ls different_versions                             # list contents of the different_versions directory
> > $ git add different_versions/*                      # add all contents of stonesoup/different_versions
> > $ git status                                    # show different_versions files in staging area
> > $ git commit -m "add stories with different objects"    # commit stonesoup/different_versions to stonesoup Git repository
> > ~~~
> > {: .bash}
> >
> > Similarly, we can ignore (as discussed later) entire directories, such as the `different_versions` directory:
> >
> > ~~~
> > $ nano .gitignore # open the .gitignore file in the texteditor to add the different_versions directory
> > $ cat .gitignore # if you run cat afterwards, it should look like this:
> > ~~~
> > {: .bash}
> >
> > ~~~
> > different_versions
> > ~~~
> > {: .output}
> >
> > To recover from this little mistake, we can just remove the `.git`
> > folder in the different_versions subdirectory. To do so we can run the following command from inside the 'different_versions' directory:
> >
> > ~~~
> > $ rm -rf different_versions/.git
> > ~~~
> > {: .bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire git-history of a project you might wanted to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}

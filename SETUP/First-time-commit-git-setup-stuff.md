# The first time you commit...

The first time you commit, you may get the following one-time message:

```
[spis15t7@ieng6-240]:spis15-aps-example:376$ git commit -m "test"
[master 00629b6] test
 Committer: Phillip Conrad <spis15t7@ieng6-240.ucsd.edu>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 2 insertions(+)
[spis15t7@ieng6-240]:spis15-aps-example:377$
```

Here's what you need to do.  Type in two commands, like this, putting in YOUR real name, and YOUR email:

```
[spis15t7@ieng6-240]:spis15-aps-example:380$ git config --global user.name "Phill Conrad"
[spis15t7@ieng6-240]:spis15-aps-example:381$ git config --global user.email "pconrad@ucsd.edu"
[spis15t7@ieng6-240]:spis15-aps-example:382$ 
```

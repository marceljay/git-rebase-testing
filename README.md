# git-rebase-testing

Step 1:
```
git checkout my-feature
```

Step 2: Rebase and mark "Commit A" to be edited:
```
git rebase -i HEAD~2               
```

Step 3: Change L.05 of A.txt, for example from `AAAA` to `0000`.

and then amend:
```
git add . && git commit --amend --no-edit && git rebase --continue
```

Step 4: Accept the incoming changes "BBBB"

Step 5:
```
git add . && git status
```
Now you should see:
```
└─$ git add . && git status
interactive rebase in progress; onto a79b1bf
Last commands done (2 commands done):
   edit 9eed66a Commit A
   pick d9e261e Commit B
No commands remaining.
You are currently rebasing branch 'my-feature' on 'a79b1bf'.
  (all conflicts fixed: run "git rebase --continue")

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   A.txt
```

It says `No commands remaining.` but if we amend, we are not amending `Commit B` but actually `Commit A`. 

Step 6: The fallacy
```
git commit --amend --no-edit && git rebase --continue`
```

Now `Commit B` was essentially squashed into `Commit A`.

What actually needs to be done is `git rebase --continue` without an amend, which will automatically jump to amending `Commit B`. 

# Git aliases
(_2021/04/09_)

Git provides an internal mechanism to define aliases.
Such a great tool to optimize your git everyday workflow!

---

I use a lot of interactive rebasing in my work. So I would often execute:
```
git rebase -i HEAD~XX
```
(_where `XX` is the number of commits that I want to focus on._)

With a simple modification to the `.gitconfig`:
```
[alias]
  r = ! sh -c \"git rebase -i HEAD~$1\" -
```

I can now simply use:
```
git r XX
```
to do the exact same thing.

---

Apart from the one above, I also added two more that I use A LOT as well:
```
[alias]
  ra = ! sh -c \"git rebase --abort\" -
[alias]
  rc = ! sh -c \"git rebase --continue\" -
```

# Multiple global git configurations
(_2020/09/15_)

If you're re-using the same machine for both personal and work-related git repositories, you might want to have different git configs for those two scenarios.

---

The simplest use-case is differentiating user identifiers (`name` & `email`), between pushing commits to personal vs work repositories.

1. Create two "sub-configs".

    1.1. One for work at `~/.gituser-work`:
    ```
    [user]
      name = Bartek Lipinski
  	  email = bartek@some_work_domain.com
    ```

    1.2. And the second one for personal stuff at `~/.gituser-default`:
    ```
    [user]
      name = Bartek Lipiński
  	  email = contact@barteklipinski.com
    ```

2. Remove any `user` related properties from `~/.gitconfig`
3. Add rules for your "sub-configs" based on the enclosing directories of your repos
```
[include]
  path = .gituser-default
[includeIf "gitdir:some_work_directory/"]
  path = .gituser-work
```

(_if the `includeIf` rule does not match, the `gituser-default` config will be used_)

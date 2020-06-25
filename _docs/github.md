

# git stash
- tmporary save modified source code
```
1) modified & tracked files
  - tracked file(already committed)
2) Staged files
  - git added files
  
  $ git stash
  $ git stash save
```
- Usage

```
- check stashed list
  $ git stash list
  
- apply(callback) stash files

  $ git stash apply               // call recent stashed files
  $ git stash apply [stash_name]
  $ git stash apply --index

- delete stash
  $ git stash drop
  $ git stash drop [stash_name]   // delete recent stashed files

- callback&delete shashed files
  $ git stash pop
  
- revert applied stash
  $ git stash show -p | git apply -R
  $ git stash show -p [stash_name] | git apply -R
```

ref : https://moon9342.github.io/jekyll-struct

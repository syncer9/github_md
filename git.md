# git.md

```
PS C:\Users\syncer9\github_md> git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean        
PS C:\Users\syncer9\github_md> git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
  remotes/origin/release


PS C:\Users\syncer9\github_md> git push origin release
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 541 bytes | 541.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/syncer9/github_md.git
   9fe7384..1f58246  release -> release

PS C:\Users\syncer9\github_md> git branch release
PS C:\Users\syncer9\github_md> git branch
* main
  release
PS C:\Users\syncer9\github_md> git checkout release
Switched to branch 'release'
PS C:\Users\syncer9\github_md> git branch
  main
* release
PS C:\Users\syncer9\github_md> git status
On branch release
nothing to commit, working tree clean

PS C:\Users\syncer9\github_md> git push origin release
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 541 bytes | 541.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/syncer9/github_md.git
   9fe7384..1f58246  release -> release


```
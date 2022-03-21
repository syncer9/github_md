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

 feature 브랜치 생성
PS C:\Users\syncer9\github_md> git checkout -b feature/v2
Switched to a new branch 'feature/v2'
PS C:\Users\syncer9\github_md> git status
On branch feature/v2
nothing to commit, working tree clean
PS C:\Users\syncer9\github_md> git branch
  dev
  feature/v1
* feature/v2
  main
  release

## feature 브랜치 원격 반영 (최초 내려받은 형상 그대로)
PS C:\Users\syncer9\github_md> git push -u origin feature/v2
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'feature/v2' on GitHub by visiting:
remote:      https://github.com/syncer9/github_md/pull/new/feature/v2
remote:
To https://github.com/syncer9/github_md.git
 * [new branch]      feature/v2 -> feature/v2
Branch 'feature/v2' set up to track remote branch 'feature/v2' from 'origin'.



```
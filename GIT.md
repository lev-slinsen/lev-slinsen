# Git

*delete selected local branches:*

`git branch | grep 'hotfix' | xargs git branch -D`

*delete selected remote branches:*

`git branch -r | awk -F/ '/\/hotfix/{print $2}' | xargs -I {} git push origin :{}`

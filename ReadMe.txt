create a sln in vs with name HelloCI
add 3 projects to sln (mvc, class library for nunit, class library for core)
project 1 - mvc - \HelloCI\src\app\HelloCI.Web
project 2 - class library - \HelloCI\src\app\HelloCI.Core
project 3 - class library - \HelloCI\src\test\HelloCI.Tests 

install git from https://git-scm.com/download/win
go to project root folder \HelloCI and run git init from bit bash
run cd .git to see .git file added by git init
run ls to list the files in .git
run cd .. to go back to go to project root folder
all files in our sln are untracked files at this point
we have to add these files to staging area so that the files can be committed and there by tracked by git
run git add . to add all the files to staging area
run git commit -m "first commit"

create a github account and create a public repository with name HelloCI
remote repo url - https://github.com/vishalch/HelloCI.git

we now need to connect local repo with remote github repo with the following command -
run git remote add origin https://github.com/vishalch/HelloCI.git

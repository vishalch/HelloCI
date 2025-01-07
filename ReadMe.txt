07Jan2025-test-commit-3

create a sln in vs with name HelloCI
add 3 projects to sln (mvc, class library for nunit, class library for core)
project 1 - mvc - \HelloCI\src\app\HelloCI.Web
project 2 - class library - \HelloCI\src\app\HelloCI.Core
project 3 - class library - \HelloCI\src\test\HelloCI.Tests 

install git from https://git-scm.com/download/win
go to project root folder \HelloCI and run git --version
configure user - git config --global user.name "vishal surve"
configure email - git config --global user.email "vishalch.surve@gmail.com" 
go to project root folder \HelloCI and run git init from bit bash
run cd .git to see .git file added by git init
run ls to list the files in .git
run cd .. to go back to go to project root folder
all files in our sln are untracked files at this point
we have to add these files to staging area so that the files can be committed and there by tracked by git
run git add . to add all the files to staging area
if the above command give error run the following command to fix the issue -
git config --global --add safe.directory C:\avishal\projects\teamcity\HelloCI
commit the untracked files - run git commit -m "first commit"

create a github account and create a public repository with name HelloCI
remote repo url - https://github.com/vishalch/HelloCI.git
url: https://github.com/login
username: Sprint..7.

we now need to connect local repo with remote github repo with the following command -
run git remote add origin https://github.com/vishalch/HelloCI.git
if the above command give error run the following command to fix the issue -
git config --global --add safe.directory C:\avishal\projects\teamcity\HelloCI

run git push -u origin master
enter github username and password or log in to your github account and rerun the above command

install TeamCity from JetBrains site
TeamCity installs with port as 8111 
serverUrl: http://localhost:8111
while installation it gives option to save agent properties at c:\teamcity\buildagent\conf\buildAgent.properties
select system account for teamcity server:
Data Directory location on the TeamCity server machine: C:\ProgramData\JetBrains\TeamCity
after installation create administrator account
	username: teamcity-admin
	password: Sprint..7.
	
install TortoiseGit from https://tortoisegit.org/
TortoiseGit provides overlay icons showing the file status, a powerful context menu for Git and much more
git exe path: C:\Program Files\Git\bin

In terms of how we define TeamCity builds
at root level we have project
within project we have a number of build configurations
so we could have bc to run unit tests and another one to run integration tests
each bc contains a number of individual build steps
example could be building a solution step, running a NUnit tests, running MSTest step, steps what will execute commands at the command line

create a project
log in to teamcity: http://localhost:8111/ | uid: teamcity-admin | pwd: Sprint..7.
click on create project button
project name: HelloCI
project id: HelloCI
description:  Hello CI Demo
click on create button

create a build configuration
click on + create build configuration button
name: HelloCI trunk
build configuration id: HelloCI_HelloCITrunk
trunk is the main line development. A good practice in version control is to call a main line as trunk or main and then you've got a branches as well as tags
branches is any short-term development
description: HelloCI trunk demo
click on create button

configure vcs root
click on + attach vcs root
vcs root name: HelloCI
type of vcs: <Guess from repository URL> or Git
vcs root name: GitVCS
vcs root id: HelloCI_GitVCS
repository url: https://github.com/vishalch/HelloCI.git
default branch: refs/heads/master
username: teamcity-admin
password: Sprint..7. 
click on create button

setting build steps
select .net
build runner: MSBuild
build file path/projects: ./HelloCI.sln
look for a path in powershell - navigate to root of the project - start . 
msbuild version: Microsoft .NET Framework 4.0
run platform: x64
click on save button

setting a build trigger
click on add new trigger link
trigger type: vcs trigger
click on save button

setting notification rules
click on my settings & tools button at top right
click on notification rules
click on windows tray notifier link
click on add a new rule link
click on checkbox - builds from the projects: HelloCI
check the following checkboxes under send notification when section
	the build fails
	the build is successful
	notify when the first error occurs
	the build starts
	the build is probably hanging
	responsibility changes
click on save button

comeover to your solution in visual studio
make a small change > commit > push
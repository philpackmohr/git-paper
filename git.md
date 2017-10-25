# Basics

Commit often, perfect later, publish once

## Comparison to other version control systems

Classical version control systems have one central repository that is accessed by all participants.

![Classical VCS](images/centralized-vcs.svg)

Each participant checks out a working copy from the central repository. Changes are committed to the central repository directly.

With Git every participant has its own full repository with all version information on his own machine.

![Classical VCS](images/distributed-vcs.svg)

This causes some advantages:

- There is no need to be connected to some central repository while working
- A participant can make commits, branches and can even change the version history on his local machine before he publishes his changes
- If a centralized VC repository gets lost you have better a backup. With Git and other decentralized VCSs every participant has a backup
- ...

## Working with Git

There are several graphical tools available that make it more or less easier to work with Git. But it is recommended to use the CLI to learn the basics. Many users prefer the CLI actually. One graphical Git tool that can be recommended is [Git Extensions](https://gitextensions.github.io/).

### Basic principles

Working with Git is much more easy and pleasant if you know some principles:

- All operations are done on the "current" branch (the branch that was checked out the last time).
- Most operations should be done with a clean working directory. This means that there should be no modifications since the last commit.
- As long as you did not publish your commits to a central one, you can change almost all of them. You can even change the order of the commits, split a commit or combine them. But do not such things on published commits if there is not a *very* good reason for that and even then you must discuss this with all people that work on the repository. If you do not follow this advice you and/or your colleagues will be irritated very much and you could be hated by all of them. 

### First steps

Make sure that you have the command `git` in your system PATH. The `git` command should be available after you installed [Git Extensions](https://gitextensions.github.io/). If there are problems or you want use only Git and nothing else you can get Git directly from its [Website](https://git-scm.com/).

Basic command syntax:

```
$ git <verb>
```

Get help:

```
$ git help <verb>
$ git <verb> --help
```

#### Create a new repository

```
PS D:\test\repo> git init
Initialized empty Git repository in D:/test/repo/.git/
```

##### With Git Extensions

Step1:

![Git Extensions step 1](images/gitext-create1.png)

Step 2:

![Git Extensions step 2](images/gitext-create2.png)

Step 3:

![Git Extensions step 3](images/gitext-create3.png)

After that you can open the Git Extensions main window.

1:

![Browse Git repository](images/gitext-browse.png)

2:

![Git Extensions main window](images/gitext-main-empty.png)

#### Add first file to repository

Add some text file to your repository directory (in this example the file is named "hello.txt" ).

Typing `git status` now will give you this output:

```
PS D:\test\repo> git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello.txt

nothing added to commit but untracked files present (use "git add" to track)
```

In Git Extensions you see this:

![Status in Git Extensions](images/gitext-1commit.png)

"Untracked" means that the file is not part of the repository yet. To add the file to the repository:

```
PS D:\test\repo> git add hello.txt
```

Alternatively you can type `git add .` but you should learn to use the ".gitignore" file before using this command.

To make a commit:

```
PS D:\test\repo> git commit -m "My first commit"
[master (root-commit) 15cc061] My first commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
```

The repository contains now exactly one commit. Typing `git status` will give you this output now:

```
PS D:\test\repo> git commit -m "My first commit"
[master (root-commit) 15cc061] My first commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
```

##### With Git Extensions

Step 1: Click on this button:

![Status in Git Extensions](images/gitext-1commit.png)

A window will open:

![Git Extensions commit window](images/gitext-commit1.png)

Step 2: Click on the button "Stage":

![Git Extensions add a file](images/gitext-commit2.png)

As seen in the image above, the file to add should be in the bottom part of the window now.

Step 3: Add a commit message and click on the button "Commit".

![Git Extensions commit done](images/gitext-commit3.png)

After confirming the message window, the Git Extensions main window should look like this:

![Git Extensions after first commit](images/gitext-main-first-commit.png)

#### Modify a file

A `git status` after a file is modified will look like this:

```
PS D:\test\repo> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   hello.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Note that Git does say nothing about "untracked" but something about "Changes not staged". It is a difference whether a file is unknown in the repository yet or a known file has modifications. The actions have to be done are similar to adding new files to the repository.

First, "stage" the file:

```
PS D:\test\repo> git add hello.txt
```

A `git status` will show that the file is ready to be committed as "modified". The actual commit is also very similar:

```
PS D:\test\repo> git commit -m "Modify a file"
[master 38b223d] Modify a file
 1 file changed, 1 insertion(+), 1 deletion(-)
```

##### With Git Extensions

Much like as the CLI, committing a modified file is very similar to committing a new file. See the description of committing a new file above.

#### Add a .gitignore file

You should add a file named `.gitignore` in the root directory of your project at the very beginning - ideally with the first commit. On [Github](https://github.com/github/gitignore) is a large collection of .gitignore files. These files cover almost all junk files that can be generated by certain languages and/or environments.

This is the ".gitignore" template for Visual Studio:

```
## Ignore Visual Studio temporary files, build results, and
## files generated by popular Visual Studio add-ons.
##
## Get latest from https://github.com/github/gitignore/blob/master/VisualStudio.gitignore

# User-specific files
*.suo
*.user
*.userosscache
*.sln.docstates

# User-specific files (MonoDevelop/Xamarin Studio)
*.userprefs

# Build results
[Dd]ebug/
[Dd]ebugPublic/
[Rr]elease/
[Rr]eleases/
x64/
x86/
bld/
[Bb]in/
[Oo]bj/
[Ll]og/

# Visual Studio 2015 cache/options directory
.vs/
# Uncomment if you have tasks that create the project's static files in wwwroot
#wwwroot/

# MSTest test Results
[Tt]est[Rr]esult*/
[Bb]uild[Ll]og.*

# NUNIT
*.VisualState.xml
TestResult.xml

# Build Results of an ATL Project
[Dd]ebugPS/
[Rr]eleasePS/
dlldata.c

# Benchmark Results
BenchmarkDotNet.Artifacts/

# .NET Core
project.lock.json
project.fragment.lock.json
artifacts/
**/Properties/launchSettings.json

*_i.c
*_p.c
*_i.h
*.ilk
*.meta
*.obj
*.pch
*.pdb
*.pgc
*.pgd
*.rsp
*.sbr
*.tlb
*.tli
*.tlh
*.tmp
*.tmp_proj
*.log
*.vspscc
*.vssscc
.builds
*.pidb
*.svclog
*.scc

# Chutzpah Test files
_Chutzpah*

# Visual C++ cache files
ipch/
*.aps
*.ncb
*.opendb
*.opensdf
*.sdf
*.cachefile
*.VC.db
*.VC.VC.opendb

# Visual Studio profiler
*.psess
*.vsp
*.vspx
*.sap

# Visual Studio Trace Files
*.e2e

# TFS 2012 Local Workspace
$tf/

# Guidance Automation Toolkit
*.gpState

# ReSharper is a .NET coding add-in
_ReSharper*/
*.[Rr]e[Ss]harper
*.DotSettings.user

# JustCode is a .NET coding add-in
.JustCode

# TeamCity is a build add-in
_TeamCity*

# DotCover is a Code Coverage Tool
*.dotCover

# AxoCover is a Code Coverage Tool
.axoCover/*
!.axoCover/settings.json

# Visual Studio code coverage results
*.coverage
*.coveragexml

# NCrunch
_NCrunch_*
.*crunch*.local.xml
nCrunchTemp_*

# MightyMoose
*.mm.*
AutoTest.Net/

# Web workbench (sass)
.sass-cache/

# Installshield output folder
[Ee]xpress/

# DocProject is a documentation generator add-in
DocProject/buildhelp/
DocProject/Help/*.HxT
DocProject/Help/*.HxC
DocProject/Help/*.hhc
DocProject/Help/*.hhk
DocProject/Help/*.hhp
DocProject/Help/Html2
DocProject/Help/html

# Click-Once directory
publish/

# Publish Web Output
*.[Pp]ublish.xml
*.azurePubxml
# Note: Comment the next line if you want to checkin your web deploy settings,
# but database connection strings (with potential passwords) will be unencrypted
*.pubxml
*.publishproj

# Microsoft Azure Web App publish settings. Comment the next line if you want to
# checkin your Azure Web App publish settings, but sensitive information contained
# in these scripts will be unencrypted
PublishScripts/

# NuGet Packages
*.nupkg
# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*
# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/
# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config
# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Microsoft Azure Build Output
csx/
*.build.csdef

# Microsoft Azure Emulator
ecf/
rcf/

# Windows Store app package directories and files
AppPackages/
BundleArtifacts/
Package.StoreAssociation.xml
_pkginfo.txt
*.appx

# Visual Studio cache files
# files ending in .cache can be ignored
*.[Cc]ache
# but keep track of directories ending in .cache
!*.[Cc]ache/

# Others
ClientBin/
~$*
*~
*.dbmdl
*.dbproj.schemaview
*.jfm
*.pfx
*.publishsettings
orleans.codegen.cs

# Since there are multiple workflows, uncomment next line to ignore bower_components
# (https://github.com/github/gitignore/pull/1529#issuecomment-104372622)
#bower_components/

# RIA/Silverlight projects
Generated_Code/

# Backup & report files from converting an old project file
# to a newer Visual Studio version. Backup files are not needed,
# because we have git ;-)
_UpgradeReport_Files/
Backup*/
UpgradeLog*.XML
UpgradeLog*.htm

# SQL Server files
*.mdf
*.ldf
*.ndf

# Business Intelligence projects
*.rdl.data
*.bim.layout
*.bim_*.settings

# Microsoft Fakes
FakesAssemblies/

# GhostDoc plugin setting file
*.GhostDoc.xml

# Node.js Tools for Visual Studio
.ntvs_analysis.dat
node_modules/

# Typescript v1 declaration files
typings/

# Visual Studio 6 build log
*.plg

# Visual Studio 6 workspace options file
*.opt

# Visual Studio 6 auto-generated workspace file (contains which files were open etc.)
*.vbw

# Visual Studio LightSwitch build output
**/*.HTMLClient/GeneratedArtifacts
**/*.DesktopClient/GeneratedArtifacts
**/*.DesktopClient/ModelManifest.xml
**/*.Server/GeneratedArtifacts
**/*.Server/ModelManifest.xml
_Pvt_Extensions

# Paket dependency manager
.paket/paket.exe
paket-files/

# FAKE - F# Make
.fake/

# JetBrains Rider
.idea/
*.sln.iml

# CodeRush
.cr/

# Python Tools for Visual Studio (PTVS)
__pycache__/
*.pyc

# Cake - Uncomment if you are using it
# tools/**
# !tools/packages.config

# Tabs Studio
*.tss

# Telerik's JustMock configuration file
*.jmconfig

# BizTalk build output
*.btp.cs
*.btm.cs
*.odx.cs
*.xsd.cs

# OpenCover UI analysis results
OpenCover/
```

# Branching

## Introduction

Branches in Git are very lightweight - each branch is just a pointer to a commit.

![Simple history](images/1-simple-history.svg)

Which branch is considered the current one is determined by the so called "HEAD" pointer. This HEAD pointer is unique inside a repository and points usually to a branch.

![Simple history with HEAD pointer](images/2-HEAD.svg)

Adding, renaming and deleting branches is nothing more than adding and deleting pointers and goes as fast (though deleting can be problematic at certain circumstances). Switching branches is more complex because your working directory must be updated to the content of the branch to switch to. But usually this goes very fast too.

If you make new commits, the "current" branch pointer (the branch pointer that is referenced by the HEAD pointer) moves automatically to the last made one.

## Creating and switching branches

One branch is always created with the first commit and has the default name "master". Besides of this, there is nothing special about the "master" branch.

To add a new branch in the repository, you jus type:

```
PS D:\test\repo> git branch topic
```

`topic` is just a name that can be chosen freely.

The repository can be considered in this state now:

![History with new branch](images/3-create-branch.svg)

You see that the repository contains now an additional branch but the HEAD pointer still points to the old one.

To actually switch the branch:

```
PS D:\test\repo> git checkout topic
Switched to branch 'topic'
```

The repository state should be now like this:

![History after switching the branch](images/4-switch-branch.svg)

The commands `git branch XXX` and `git checkout XXX` can be combined to:

```
PS D:\test\repo> git checkout -b XXX
Switched to a new branch 'XXX'
```

## Committing on branches

After you switched the branch you can commit your changes as usual. After making a commit, the repository will look like this:

![Commits on another branch](images/5-advance-topic.svg)

The "current" branch pointer advances with your commits while other branch pointers are not touched. If you switch the branch again (assume "master" in this example) the working directory will be set to the state where the last commit was made on this branch.

![Switched back to master](images/6-back-to-master.svg)

If you now make a commit on the "master" branch, the history will split:

![Split history](images/7-advance-master.svg)

# Merging

# Rebase

# Working with central repositories

# Workflows

## Practice

# Some technical background

## About repositories

A personal Git repository is nothing more then a directory that contains a subdirectory named ".git" and with certain content. This subdirectory contains all the information about the repository.

# Sources

[Git workshop of Alexander Groß](https://github.com/agross/git-reveal)

[Book "Pro Git"](https://git-scm.com/book/en/v2)
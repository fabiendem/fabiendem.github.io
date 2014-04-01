---
layout: post
title: "Get the Git working branch in Gradle"
date: 2014-03-17 15:49:45 +0000
comments: true
categories: 
- Android
- Gradle
---

Getting the working branch name via Gradle can be useful if you want to add this information somewhere in your build, for example in the versionName of your debug Android build by suffixing it.

<!-- more -->

``` groovy
buildTypes {
    debug {
        ...
        versionNameSuffix "-branch_" + getWorkingBranch()
        ...
    }
    ...
}
```
The getWorkingBranch is a function defined as below in your build.gradle file: 
``` groovy
/**
 * Get the name of the working branch of the project
 *
 * @return Name of the working branch
 */
def getWorkingBranch() {
    // Triple double-quotes for the breaklines
    def workingBranch = """git --git-dir=${rootDir}/../.git
                               --work-tree=${rootDir}/..
                               rev-parse --abbrev-ref HEAD""".execute().text.trim()
    print "Working branch: " + workingBranch
    return workingBranch
}
```

**Source:** Figured it out from the [Jake Wahrton Google+ post](https://plus.google.com/+JakeWharton/posts/6f5TcVPRZij) and the comments.

It actually executes the following git command to get the current branch: `git rev-parse --abbrev-ref HEAD`

`--git-dir=${rootDir}/.git --work-tree=${rootDir}` is used to tell git on which local repo the command should be executed, as the gradle function (and so the git command) won't be executed from the root of you Android project. You just need to show its way to git...

If your module executing the getWorkingBranch task is 2 levels down within your project, simply update the `--git-dir=${rootDir}/.git --work-tree=${rootDir}` parameters to   
`--git-dir=${rootDir}/../../.git --work-tree=${rootDir}/../..` (see the `../..`)

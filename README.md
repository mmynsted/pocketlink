pocketlink
==========

Manage files/directories, controlled by git, by abscracting the project deliverables into pockets 

## Requires
* unix like OS with bash shell
* [git-archive-all](https://github.com/Kentzo/git-archive-all)
                                                                                                                                                                                                                                                                                
##Background
Pocketlink was designed to address a particular problem.  The problem was that I wanted to manage multiple shell scripts and applications in separate git repositories but have the deployment files live in the same destination directory or location in my path.  I also wanted the deployment files to reflect a particular commit.  This would permit me to separate production and test deployments in a way that would not otherwise be possible.  I wanted to be able to automate deployment by running a simple shell command.  The final piece of the pie was that I wanted to be able to look somewhere and see from what repository a deployment originated.                                                                                                                                                                      
                                                                                                                                                                                                                                                                                
##Use                                                                                                                                                                                                                                                                           
Execute pocketlink in the top of the git repository you wish to export.  Provide pocketlink with the fully qualified destination directory as the '-d ' parameter.                                                                                                              

Example                                                                                                                                                                                                                                                                        
``` 
$pocketlink -d /user/myuser/bin
```
                                                                                                                                                                                                                                                 
##Detail
Pocketlink is used to export all of the files from an active branch of a git repository to a source directory under the pocket tree.  The pocket tree is a directory tree that contains a directory for each exported git repository and defaults to '~/pocket'.  One may examine the pocket directory to understand the alignment between destination files and and source repositories.                                                                                                                                                                       
                                                                                                                                                                                                                                                                                
The source directory is used as a source for pocketlink files.  This source directory is git repository directory with the branch we wish to deploy being the active branch.  This directory should be the working directory when pocketlink is executed.  Recall that the source directory is a git repository, thus to prevent a file from being exported, create a .gitattributes file using the 'export-ignore' keyword.                                                                                                                                    
                                                                                                                                                                                                                                                                                
Example .gitattributes:
```                                                                                                                                                                                                                                                         
NoExportMe.txt   export-ignore
```                                                                                                                                                                                                                                                  

The destination directory is the deployment destination.  It will be populated with symbolic links back to a pocketlink directory.  It is possible, of course to have the same destination directory be used for more than one pocketlink.  Think of an example where two different shell scripts are deployed to the same bin directory, but are managed by two different git repositories and thus two different pocklinks.                                                                                                                                   
                                                                                                                                                                                                                                                                                
A pocketlink directory is a directory located under the pocket directory.  A pocketlink directory will be created in alignment with a git repository, such that a directory will exist for each git repository used as a source.  It is possible for more than one pocketlink directory to use the same deployment directory.  Pocketlink creates a  file is in each pocketlink directory called 'pocketlink-readme.txt'.  This file simply documents the source repository and deployment destination defined for the given pocketlink.                        
                                                                                                                                                                                                                                                                                
One thing that pocketlink will not do is a sanity check to ensure you do not deploy files of the same name to the same path.                                                                                                                                                    
                                                                                                                                                                                                                                                                                
Example:                                                                                                                                                                                                                                                                        
```                                                                                                                                                                                                                                                                             
git repository   source              destination   deployment
--------------   ----------------    ------------  -------------
gitrepA          ~/pocket/gitrepA    ~/bin         ~/bin/coolScript
gitrepB          ~/pocket/gitrepB    ~/bin         ~/bin/scriptB
gitrepC          ~/pocket/gitrepC    ~/bin         ~/bin/coolScript
gitrepD          ~/pocket/gitrepD    ~/bin         ~bin/scriptD
```
                                                                                                                                                                                                                                                                             
In the above example gitrepA and gitrepC have the same deployment file name 'coolScript' and are using the same destination directory.  This type of collision must be avoided.  Pocketlink will not prevent nor check for such a collision. It is up to you the user to prevent these collisions.  Just as one would need to prevent path collisions.                                                                                                                                                                                                          
                                                                                                                                                                                                                                                                                
Each time that pocklink is run from the same source directory with the same parameters, it will first attempt remove the old deployment so it may be replaced with the new deployment.  This should make it simple refresh deployments based on new commits.                    
                                                                                                                                                                                                                                                                                
Use at your own risk, and good luck.  :-) 

## License: MIT


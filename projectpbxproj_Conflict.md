

merge issues.


# what I learn. 

      when working at 2 branches create files, and folders, don't move things around it will created
      conflicts in pbxproj ("It is responsible for maintaining references to all of the linked files and their groupings, 
                            linked frameworks, and most importantly, the project's build settings

# how to solve it

      choose which reference to use from one of the branches, or union the branch.




how did it happen.


master branch to 

1. subbranch1  (add files and change folder structure in Xcode)
2. subbranch2 (add files and change folder structure in Xcode)


how the problem is solved

create a 3rd branch from master (to test if things will workout)

merge subbranch1. (some conflicts project file) I think this is where Xcode record the folder and file structure. i.e. which files belongs to this branch
merge subbranch2. (look at each conflict)

so weird conflict.

example


folderName             folderName

Xcode tell you there is a conflict this can happen when in branch 1 and 2 same folder name are created in different subfolders….
In this case i created a empty folder in on of the branches (was going to move the file manually)

solution: i think go back to one of the subbranches, rename the folder than you probably will not have this problem


so, not so sure, but I decided to merge the file and union the conflicts.

first try. corrupted the file ….. -> discard all changes 

2nd try. when show conflict with exact same folderName, I randomly selected from one branch , it the end all the files was move to that new folder.

conclusion:
i think the problem isn’t as complicated as first thought, git keep track of files changes pretty well, and there wasn’t really any problems there
the problem have to do with how xcode record it’s files structures.


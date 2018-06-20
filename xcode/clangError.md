**Dealing with Clang Error in XCode **


the easiest solution to this is to delete both pods folder and podfile.lock file


in terminal do → pod install

this will reinstall the Pods folder and create a new Podfile.lock it will help reindex all the files in Xcode


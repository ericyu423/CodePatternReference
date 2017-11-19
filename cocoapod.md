# Problem and solutions Mac OS High Sierra 

lexicons:
sudo - super user do (similar to windows run as administrator)
rvm - Ruby Verion Manager
gem - a gem is a library that contains a specific piece of functionality+ files and assets

past problems:
  Don't update/fix cocoapod in project directory sure it can fix the problem, but when creating new project you get
  the same problems again


1. Ruby Version Manager (RVM) RVM 

          rvm get stable
  
  
2.  sudo gem update   

          sudo gem update --system

# Make sure you install at the right directory 

          sudo gem install -n /usr/local/bin cocoapods
          pod install



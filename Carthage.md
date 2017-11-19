# much easier to use than cocoapods

//it always take forever to get cocoapods setup correct 


#install 

$ brew update
$ brew install carthage

#create proj cd 

touch Cartfile

open -a Xcode Cartfile

github "drmohundro/SWXMLHash" ~> 4.0

carthage update --platform iOS




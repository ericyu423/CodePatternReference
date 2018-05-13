# sublime command line launch setup



go to the folder you want to launch example

step1

    ->cd /Users/ericyu423/Desktop/ReactNative/Projs/albums

step2

    -> /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl .t
    ->
      export PATH=/bin:/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin:$PATH
      export EDITOR='subl -w'
      
      cd /usr/local/bin
      
      ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl
      
      
      
step3.
  subl . now can launch proj in command line just like atom .

# Atom setup


Linter allow you to plug in different Linters



open project add/open project folder /albums <--proj that you created last time

1. install lints
  Atom->Preference ->install -> serach linter-eslint, also install linter
2. install preset preference
  npm install --save-dev eslint-config-rallycoding
  
3. create file in proj file name .eslintrc // this is project specific settings
      every proj will need this if we want to use eslint
      
      {
          "extends": "rallycoding"
      }
 
# Sublime seteup
//npm node package manager
    
    1.  sudo npm install -g eslint  //globally install lint
    
    2. package controll
       open sublime, open /albums proj folder
       view -> show console -> paste below code from https://packagecontrol.io/installation
    
    
          import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60';
          pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); 
          urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) );
          by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); 
          dh = hashlib.sha256(by).hexdigest(); 
          print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)



    3. install config with npm
        in terminal inside proj folder
        npm install --save-dev eslint-config-rallycoding //just like what we did with atom...i guess we don't need to do it again
     4. create file .eslintrc //just like last time, if we did it for atom no need to do it again   

      5. add linter and eslint (atom you can just click for sumblime we use package control)
          a. command + shift + p
             -> install package (enter)
             -> sublime linter
             -> Install SublimeLinter-contrib-eslint //can't find this for some reason
             ->SublimeLinter-eslint
             
          




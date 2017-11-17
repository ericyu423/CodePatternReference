# steps


1.( after create project) Add new target pick, Share Extension.  (square box with an up arrow)
    - this is in it own sandbox
    - this creates _ViewController: SLComposeServiceViewController
2. Create App Group to share data between sandboxeses

 
    - login apple devleoper -> Identifier -> app group -> ID (group.ShareApp.example) string of your choice
    - go back to turn on add on "group.ShareApp.example" in App Groups
    
3. edit plist on shareExtension

              <key>NSExtension</key>
                <dict>

                      <key>NSExtensionAttributes</key>
                      <dict>
                          <key>NSExtensionActivationRule</key>
                          <dict>
                              <key>NSExtensionActivationSupportsImageWithMaxCount</key>
                              <integer>1</integer>
                          </dict>
                      </dict>

                  <key>NSExtensionMainStoryboard</key>
                  <string>MainInterface</string>
                  <key>NSExtensionPointIdentifier</key>
                  <string>com.apple.share-services</string>
                </dict>


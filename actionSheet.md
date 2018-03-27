
#action sheet to log out


        private func setupLogOutButton(){
              navigationItem.rightBarButtonItem = UIBarButtonItem(image: #imageLiteral(resourceName: "gear")
                  .withRenderingMode(.alwaysOriginal),style: .plain, target: self,action: #selector(settingClicked))
          }

          @objc private func settingClicked(){
              let alertController = UIAlertController(title: "Log out", message: "Are you sure", preferredStyle: .actionSheet)

              alertController.addAction(UIAlertAction(title: "Log out", style: .destructive, handler: { (_) in
                  print ("perform log out")

                  }))

              alertController.addAction(UIAlertAction(title: "Cancel", style: .cancel, handler: nil))

                  present(alertController, animated: true, completion: nil)

          }

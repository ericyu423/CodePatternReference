#  ALL ABOUT TEXTFIELD

#  Most Basic Way:  Clicking Outside Or Other TextField Activate @IBAction func

         @IBAction func field1(_ sender: UITextField) {

          }

          @IBAction func field2(_ sender: UITextField) {

          }

          override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {

              self.view.endEditing(true)

          }
    
    
 #  With Delegation 


                   //
                  //  ViewController.swift
                  //  TestToBeDeletedSOon
                  //
                  //  Created by eric yu on 5/18/17.
                  //  Copyright © 2017 eric yu. All rights reserved.
                  //

                  import UIKit

                  class ViewController: UIViewController, UITextFieldDelegate {

                      var textfield0 =  UITextField()
                      var textfield1 =  UITextField()
                      var textfield2 =  UITextField()
                      var textfield3 =  UITextField()

                      override func viewDidLoad() {
                          super.viewDidLoad()
                          setupTextFields()
                      }

                      override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
                          self.view.endEditing(true)
                      }
                  }

                  //MARK: - UITextFieldDelegate

                  extension ViewController {
                      func textFieldDidEndEditing(_ textField: UITextField) {
                          //id currentfield by
                          //1. tag number
                          //2. compare textField to textField0,1,2..ect
                      }

                      func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
                          return true
                      }

                      func textFieldShouldReturn(_ textField: UITextField) -> Bool {
                          return true
                      }

                  }

                  extension ViewController {
                      func setupTextFields(){
                          textfield0.delegate = self
                          textfield1.delegate = self
                          textfield2.delegate = self
                          textfield3.delegate = self

                          textfield0.tag = 0
                          textfield1.tag = 1
                          textfield2.tag = 2
                          textfield3.tag = 3

                          textfield0.borderStyle = .roundedRect
                          textfield1.borderStyle = .roundedRect
                          textfield2.borderStyle = .roundedRect
                          textfield3.borderStyle = .roundedRect

                          view.addSubview(textfield0)
                          view.addSubview(textfield1)
                          view.addSubview(textfield2)
                          view.addSubview(textfield3)

                          textfield0.anchor(top: topLayoutGuide.bottomAnchor, left: view.leftAnchor, bottom: nil, right: view.rightAnchor, paddingTop: 10, paddingLeft: 30, paddingBottom: 0, paddingRight: 30, width: 0, height: 30)

                          textfield1.anchorToTopView(viewOnTop: textfield0, paddingTop: 30)
                          textfield2.anchorToTopView(viewOnTop: textfield1, paddingTop: 30)
                          textfield3.anchorToTopView(viewOnTop: textfield2, paddingTop: 30)
                      }
                  }


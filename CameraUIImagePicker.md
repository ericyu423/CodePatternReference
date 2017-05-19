#  Pick Image from Phone Or Camera (don't forget to edit info.plist)

        //
        //  ViewController.swift
        //  Camera
        //
        //  Created by eric yu on 5/19/17.
        //  Copyright © 2017 eric yu. All rights reserved.
        //



      import UIKit

      class ViewController: UIViewController,UIImagePickerControllerDelegate,UINavigationControllerDelegate {

          var image: Any!

          let button: UIButton = {
              let button = UIButton()
              button.setTitle("take photo", for: .normal)
              button.addTarget(nil, action: #selector(handleCamera), for: .touchUpInside)


              return button
          }()

          override func viewDidLoad() {
              super.viewDidLoad()
              view.addSubview(button)
              button.anchorToVCEdege(type_self: self)
          }


          func handleCamera(){
              //plist add 
              //"Privacy - Photo Library Usage Description"
              let imagePickerController = UIImagePickerController()
              present(imagePickerController, animated: true, completion: nil)
              imagePickerController.delegate = self
              imagePickerController.allowsEditing = true

          }

          func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {


              image = info[UIImagePickerControllerOriginalImage] ??  info[UIImagePickerControllerEditedImage]

              button.setImage((image as! UIImage).withRenderingMode(.alwaysOriginal), for: .normal)

              //convert to data for saving

              let resizeImage = (image as! UIImage).resized(withPercentage: 0.5)
              let data = UIImagePNGRepresentation(resizeImage!)

              //covert back to image
              image = UIImage(data:data!,scale:1.0)

              dismiss(animated: true, completion: nil)
          }
      }

      //extension from stackoverflow not my 

      extension UIImage {
          func resized(withPercentage percentage: CGFloat) -> UIImage? {
              let canvasSize = CGSize(width: size.width * percentage, height: size.height * percentage)
              UIGraphicsBeginImageContextWithOptions(canvasSize, false, scale)
              defer { UIGraphicsEndImageContext() }
              draw(in: CGRect(origin: .zero, size: canvasSize))
              return UIGraphicsGetImageFromCurrentImageContext()
          }
          func resized(toWidth width: CGFloat) -> UIImage? {
              let canvasSize = CGSize(width: width, height: CGFloat(ceil(width/size.width * size.height)))
              UIGraphicsBeginImageContextWithOptions(canvasSize, false, scale)
              defer { UIGraphicsEndImageContext() }
              draw(in: CGRect(origin: .zero, size: canvasSize))
              return UIGraphicsGetImageFromCurrentImageContext()
          }
      }

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

                    var imageView:UIImageView = {
                        let iv = UIImageView()
                        iv.backgroundColor = .gray
                        return iv
                    }()

                    let takebutton: UIButton = {
                        let button = UIButton()
                        button.setTitle("take photo", for: .normal)
                        button.addTarget(nil, action: #selector(takePhoto), for: .touchUpInside)
                        button.backgroundColor = .gray
                        return button
                    }()
                    let pickButton: UIButton = {
                        let button = UIButton()
                        button.setTitle("select photo", for: .normal)
                        button.addTarget(nil, action: #selector(getPhoto), for: .touchUpInside)
                        button.backgroundColor = .gray
                        return button
                    }()


                    override func viewDidLoad() {
                        super.viewDidLoad()
                        view.addSubview(imageView)
                        view.addSubview(takebutton)
                        view.addSubview(pickButton)

                        imageView.anchor(top: topLayoutGuide.topAnchor, left: view.leftAnchor, bottom: nil, right: view.rightAnchor, paddingTop: 0, paddingLeft: 0, paddingBottom: 0, paddingRight: 0, width: 0, height: view.frame.height - 100)

                        takebutton.anchorToTopView(viewOnTop: imageView, paddingTop: 5)
                        pickButton.anchorToTopView(viewOnTop: takebutton, paddingTop: 5)


                    }

                    func takePhoto(){
                        let imagePicker = UIImagePickerController()
                        imagePicker.delegate = self
                        imagePicker.allowsEditing = true
                        if UIImagePickerController.isSourceTypeAvailable(.camera){
                            imagePicker.sourceType = .camera
                            present(imagePicker, animated: true, completion: nil)
                        }
                    }
                    func getPhoto(){
                        let imagePicker = UIImagePickerController()
                        imagePicker.delegate = self
                        imagePicker.allowsEditing = true
                        imagePicker.sourceType = .photoLibrary  //.savedPhotosAlbum
                        present(imagePicker, animated: true, completion: nil)
                    }

                    func imagePickerControllerDidCancel(_ picker: UIImagePickerController) {
                        picker.dismiss(animated: true, completion: nil)
                    }

                    func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {


                        image = info[UIImagePickerControllerEditedImage] ?? info[UIImagePickerControllerOriginalImage]

                        imageView.image = image as? UIImage


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


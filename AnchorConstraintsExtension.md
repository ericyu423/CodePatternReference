
          //
          //  AnchorExtension.swift
          //  TestToBeDeletedSOon
          //
          //  Created by eric yu on 5/18/17.
          //  Copyright © 2017 eric yu. All rights reserved.
          //


          import UIKit
          extension UIView {

              func anchorTopView(viewOnTop v: UIView,paddingTop p: CGFloat){

                  translatesAutoresizingMaskIntoConstraints = false

                  self.topAnchor.constraint(equalTo: v.bottomAnchor, constant: p).isActive = true
                  self.leadingAnchor.constraint(equalTo: v.leadingAnchor, constant: 0).isActive = true

                  self.trailingAnchor.constraint(equalTo: v.trailingAnchor, constant: 0).isActive = true

                  self.heightAnchor.constraint(equalTo: v.heightAnchor, multiplier: 0)

              }

              func anchorToCenter(x: NSLayoutXAxisAnchor?, y: NSLayoutYAxisAnchor?,offsetX: CGFloat, offsetY: CGFloat,width: CGFloat, height: CGFloat){
                  translatesAutoresizingMaskIntoConstraints = false
                  if let x = x {
                      self.centerXAnchor.constraint(equalTo: x, constant: offsetX).isActive = true
                  }
                  if let y = y {
                      self.centerYAnchor.constraint(equalTo: y, constant: offsetY).isActive = true
                  }
                  if width != 0 {
                      widthAnchor.constraint(equalToConstant: width).isActive = true
                  }
                  if height != 0 {
                      heightAnchor.constraint(equalToConstant: height).isActive = true
                  }
              }

              func anchorToVCEdege(type_self vc: UIViewController) {
                  translatesAutoresizingMaskIntoConstraints = false
                  //Note:  view.layoutMarginsGuide.trailingAnchor
                  //       provide about 8 standard space right edge
                  //       currently not used
                  //let margin = vc.view.layoutMarginsGuide

                  self.topAnchor.constraint(equalTo: vc.topLayoutGuide.topAnchor, constant: 0).isActive = true
                  self.leadingAnchor.constraint(equalTo: vc.view.leadingAnchor, constant: 0).isActive = true
                  self.trailingAnchor.constraint(equalTo: vc.view.trailingAnchor, constant: 0).isActive = true
                  self.bottomAnchor.constraint(equalTo: vc.bottomLayoutGuide.bottomAnchor, constant: 0).isActive = true

              }
              func anchorToViewEdeges(parentView: UIView) {
                  translatesAutoresizingMaskIntoConstraints = false

                  self.topAnchor.constraint(equalTo: parentView.topAnchor, constant: 0).isActive = true
                  self.leftAnchor.constraint(equalTo: parentView.leftAnchor, constant: 0).isActive = true
                  self.rightAnchor.constraint(equalTo: parentView.rightAnchor, constant: 0).isActive = true
                  self.bottomAnchor.constraint(equalTo: parentView.bottomAnchor, constant: 0).isActive = true

              }

              func anchor(top: NSLayoutYAxisAnchor?, left: NSLayoutXAxisAnchor?, bottom: NSLayoutYAxisAnchor?, right: NSLayoutXAxisAnchor?,  paddingTop: CGFloat, paddingLeft: CGFloat, paddingBottom: CGFloat, paddingRight: CGFloat, width: CGFloat, height: CGFloat) {

                  translatesAutoresizingMaskIntoConstraints = false

                  if let top = top {
                      self.topAnchor.constraint(equalTo: top, constant: paddingTop).isActive = true
                  }

                  if let left = left {
                      self.leftAnchor.constraint(equalTo: left, constant: paddingLeft).isActive = true
                  }

                  if let bottom = bottom {
                      bottomAnchor.constraint(equalTo: bottom, constant: -paddingBottom).isActive = true
                  }

                  if let right = right {
                      rightAnchor.constraint(equalTo: right, constant: -paddingRight).isActive = true
                  }

                  if width != 0 {
                      widthAnchor.constraint(equalToConstant: width).isActive = true
                  }

                  if height != 0 {
                      heightAnchor.constraint(equalToConstant: height).isActive = true
                  }
              }
          }

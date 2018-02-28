source: https://github.com/luismachado/Swift/blob/master/PickerLabels.swift



          import Foundation
          import UIKit


          extension UIPickerView {

              func setPickerLabels(labels: [Int:UILabel], containedView: UIView) { // [component number:label]

                  let fontSize:CGFloat = 20
                  let labelWidth:CGFloat = containedView.bounds.width / CGFloat(self.numberOfComponents)
                  let x:CGFloat = self.frame.origin.x
                  let y:CGFloat = (self.frame.size.height / 2) - (fontSize / 2)

                  for i in 0...self.numberOfComponents {

                      if let label = labels[i] {

                          if self.subviews.contains(label) {
                              label.removeFromSuperview()
                          }

                          label.frame = CGRect(x: x + labelWidth * CGFloat(i), y: y, width: labelWidth, height: fontSize)
                          label.font = UIFont.boldSystemFont(ofSize: fontSize)
                          label.backgroundColor = .clear
                          label.textAlignment = NSTextAlignment.center

                          self.addSubview(label)
                      }
                  }
              }
          }

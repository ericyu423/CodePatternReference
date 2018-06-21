


        //
        //  ViewController.swift
        //  MVVMwithCADisplayLink
        //
        //  Created by eric yu on 6/21/18.
        //  Copyright © 2018 eric yu. All rights reserved.
        //

        import UIKit

        class ViewController: UIViewController {

            let countingLabel: UILabel = {
                let label = UILabel()
                label.text = "1234"
                label.font = UIFont.boldSystemFont(ofSize: 18)
                return label
            }()

            private var displayLink: CADisplayLink?


            override func viewDidLoad() {
                super.viewDidLoad()
                view.addSubview(countingLabel)
                countingLabel.frame = view.frame

                //create CADisplayLink
                displayLink = CADisplayLink(target: self, selector: #selector(handleUpdate))

                displayLink?.add(to: .main, forMode: .defaultRunLoopMode) //most command runloop probalby 60 frame / sec


            }
            var startValue:Double = 0
            let endValue:Double = 1000
            let animationDuration: Double = 1.5
            let animationStartDate = Date()


            @objc func handleUpdate(){
                //this is like the loop function inside openGL
        //        let seconds = Date().timeIntervalSince1970
        //        self.countingLabel.text = "\(seconds)"

                let now = Date()
                let elapsedTime = now.timeIntervalSince(animationStartDate)

                if elapsedTime > animationDuration {
                    self.countingLabel.text = "\(endValue)"

                    //done this can be in a diff function
                    displayLink?.invalidate()
                    displayLink = nil
                }else{
                    let percentage = elapsedTime / animationDuration

                    let value = percentage * (endValue - startValue)
                    self.countingLabel.text = "\(value)"
                }

            }
        }


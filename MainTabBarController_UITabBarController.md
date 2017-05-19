#  MainTabBarController: UITabBarController  (You Do Not SubClass UITabBarController If Storyboard Are Used)
//
//
//
//
#  Examples: To link add UIViewController inside viewControllers = [...]  You can have single vc if you wish

            //
            //  MainTabBarController.swift
            //  ProjectStarterKit
            //
            //  Created by eric yu on 5/17/17.
            //  Copyright © 2017 eric yu. All rights reserved.
            //

            import UIKit

            class MainTabBarController: UITabBarController,UICollectionViewDelegateFlowLayout {
                override func viewDidLoad() {
                    super.viewDidLoad()

                    //regular view not embeded in Navigation Controller
                    let vc: UIViewController = {
                        let vc = ViewController()
                        vc.tabBarItem.title = "view"
                        //you can give tabBarItem a tag number if you want
                        vc.tabBarItem = UITabBarItem(tabBarSystemItem: UITabBarSystemItem.featured, tag: 1)
                        //title get override by systemItem

                        return vc
                    }()

                    //embeded in Navigation Controller
                    let bvc: UIViewController = {

                        let vc = UINavigationController(rootViewController: BaseViewController())
                         vc.tabBarItem = UITabBarItem(tabBarSystemItem: UITabBarSystemItem.contacts, tag: 2)
                        vc.tabBarItem.title = "base view"
                        return vc
                    }()

                    //embeded in Navigation Controller go to CollectionView
                    let cv: UINavigationController = {
                        let vc = UINavigationController(rootViewController: CollectionViewController())
                        vc.tabBarItem.image = #imageLiteral(resourceName: "eye")
                         vc.tabBarItem.title = "collection"

                        return vc
                    }()

                    //embeded in Navigation Controller go to TableVew
                    let tv: UINavigationController = {
                        let vc = UINavigationController(rootViewController: TableViewController())

                         vc.tabBarItem.image  = #imageLiteral(resourceName: "eye")
                         vc.tabBarItem.title = "table"

                        return vc
                    }()

                    tabBar.tintColor = .black
                    //The following connect vc to bar buttons
                    viewControllers = [vc,bvc,cv,tv]
                }
            }

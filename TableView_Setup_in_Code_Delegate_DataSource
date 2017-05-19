
            //
            //  TableViewController.swift
            //  ProjectStarterKit
            //
            //  Created by eric yu on 5/17/17.
            //  Copyright © 2017 eric yu. All rights reserved.
            //

            import UIKit

            class TableViewController: UIViewController,UITableViewDelegate,UITableViewDataSource {

                let testArray = [1,2,3,4,5,6,7,8,9,10]
                lazy var tableView:UITableView = {
                    let tv = UITableView()
                    tv.delegate = self
                    tv.dataSource = self
                    tv.translatesAutoresizingMaskIntoConstraints = false
                   return tv
                }()
                override func viewDidLoad() {
                    super.viewDidLoad()

                    tableView.register(UITableViewCell.self, forCellReuseIdentifier: "cell")
                    layoutTable()
                    // Do any additional setup after loading the view.
                }
                func layoutTable(){
                    view.addSubview(tableView)

                    tableView.topAnchor.constraint(equalTo: topLayoutGuide.topAnchor, constant: 0).isActive = true
                    tableView.bottomAnchor.constraint(equalTo: bottomLayoutGuide.topAnchor, constant: 0).isActive = true
                    tableView.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 0).isActive = true
                    tableView.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: 0).isActive = true
                }
            }

            extension TableViewController {

                //control click on UITableViewDelegate will let you know
                //exactly which methods you need 

                func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
                    return testArray.count
                }

                func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell{
                    let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
                    cell.textLabel?.text = "\(testArray[indexPath.row])"
                    return cell
                }
            }

          //
          //  CollectionViewController.swift
          //  ProjectStarterKit
          //
          //  Created by eric yu on 5/17/17.
          //  Copyright © 2017 eric yu. All rights reserved.
          //

          import UIKit

          class CollectionViewController: UIViewController,UICollectionViewDataSource,UICollectionViewDelegate{

              lazy var collectionView: UICollectionView = {
                  var layout = UICollectionViewFlowLayout()
                  layout.sectionInset = UIEdgeInsets(top: 10, left: 10, bottom: 10, right: 10)
                  layout.itemSize = CGSize(width: 50, height: 50)

                  let cv = UICollectionView(frame: .zero, collectionViewLayout: layout)
                  cv.translatesAutoresizingMaskIntoConstraints = false
                  cv.delegate = self
                  cv.dataSource = self
                  cv.backgroundColor = .red
                  return cv
              }()


              override func viewDidLoad() {
                  super.viewDidLoad()


                  collectionView.register(UICollectionViewCell.self, forCellWithReuseIdentifier: "cell")
                  collectionView.register(UICollectionReusableView.self, forSupplementaryViewOfKind: UICollectionElementKindSectionHeader, withReuseIdentifier: "cell")

                  layoutCollectionView()
              }

              func layoutCollectionView()
              {
                  view.addSubview(collectionView)
                  collectionView.topAnchor.constraint(equalTo: topLayoutGuide.topAnchor, constant: 0).isActive = true
                  collectionView.bottomAnchor.constraint(equalTo: bottomLayoutGuide.topAnchor, constant: 0).isActive = true
                  collectionView.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 0).isActive = true
                  collectionView.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: 0).isActive = true
              }

          }

          extension CollectionViewController: UICollectionViewDelegateFlowLayout {
              func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, referenceSizeForHeaderInSection section: Int) -> CGSize {//width doesn't matter it will get set to default frame width
                  return CGSize(width: .allZeros, height: 200)
              }
              func collectionView(_ collectionView: UICollectionView, viewForSupplementaryElementOfKind kind: String, at indexPath: IndexPath) -> UICollectionReusableView {
                  let cell = collectionView.dequeueReusableSupplementaryView(ofKind: UICollectionElementKindSectionHeader, withReuseIdentifier: "cell", for: indexPath)
                  cell.backgroundColor = .purple
                  return cell
              }

             func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int
              {
                  return 10
              }
              func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell{

                  let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "cell", for: indexPath)

                  cell.backgroundColor = .green
                  return cell
              }

               func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
                  return CGSize(width: 50, height: 50)
               }
          }

          extension CollectionViewController {
              //UICollectionViewDelegateFlowLayout  is not need if you do the following
              //  var layout = UICollectionViewFlowLayout()
              //  layout.sectionInset = UIEdgeInsets(top: 10, left: 10, bottom: 10, right: 10)
              //  let cv = UICollectionView(frame: .zero, collectionViewLayout: layout)

              //UICollectionViewDelegateFlowLayout 

              //methods
              /*
               func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {

               return CGSize(width: 50, height: 50)
               }*/
          }

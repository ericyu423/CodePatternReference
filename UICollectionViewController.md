<p align="center">
  <img src="https://github.com/ericyu423/CodePatternReference/blob/master/image/collectionView.png" width="300"/>
</p>




                    import UIKit

                    class PhotoSelectorController: UICollectionViewController,UICollectionViewDelegateFlowLayout{
                        let cellId = "cellId"
                        let headerId = "headerId"

                        override func viewDidLoad(){
                            super.viewDidLoad()
                            collectionView?.backgroundColor = .yellow

                            setupNavigationButton()

                            //register cell
                            collectionView?.register(UICollectionViewCell.self, forCellWithReuseIdentifier: cellId)

                            //register header
                             collectionView?.register(UICollectionViewCell.self, forSupplementaryViewOfKind: UICollectionElementKindSectionHeader, withReuseIdentifier: headerId)

                        }


                        private func setupNavigationButton(){
                            navigationController?.navigationBar.tintColor = .black
                            navigationItem.leftBarButtonItem = UIBarButtonItem(title: "Cancel", style: .plain, target: self, action: #selector(handleCancel))
                             navigationItem.rightBarButtonItem = UIBarButtonItem(title: "Next", style: .plain, target: self, action: #selector(handleNext))
                        }
                        @objc private func handleCancel(){
                            dismiss(animated: true,completion: nil)
                        }
                        @objc private func handleNext(){
                            dismiss(animated: true,completion: nil)
                        }

                    }

                    //collecdtionViewFlowLayout delegate
                    extension PhotoSelectorController {
                        func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, minimumInteritemSpacingForSectionAt section: Int) -> CGFloat {
                            return 1
                        }
                        func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, minimumLineSpacingForSectionAt section: Int) -> CGFloat {
                            return 1
                        }
                        func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {

                            //-3 because there are 3 black lines that are 1 pixel wide inbetween each collection view
                            let width = (view.frame.width - 3 ) / 4
                            return CGSize(width: width, height: width)
                        }
                    }

                    //collectionView delegate functions
                    extension PhotoSelectorController {
                        func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, referenceSizeForHeaderInSection section: Int) -> CGSize {
                            let width = view.frame.width
                            return CGSize(width: width, height: width)
                        }
                        //this function will show only if referenceSizeForFooter is called
                        override func collectionView(_ collectionView: UICollectionView, viewForSupplementaryElementOfKind kind: String, at indexPath: IndexPath) -> UICollectionReusableView {
                            let header = collectionView.dequeueReusableSupplementaryView(ofKind: kind, withReuseIdentifier: headerId, for: indexPath)
                            header.backgroundColor = .red
                            return header
                        }
                        override func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
                            return 5
                        }
                        override func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
                            let cell = collectionView.dequeueReusableCell(withReuseIdentifier: cellId, for: indexPath)
                            cell.backgroundColor = .blue
                            return cell
                        }
                        override var prefersStatusBarHidden: Bool {
                            return true
                        }

                    }



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


<p align="center">
<img src="https://github.com/ericyu423/CodePatternReference/blob/master/image/collectionViewWithLine.png" width="300"/>
</p>
  
# add insect to have a line that seperate header view

      func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, 
                          insetForSectionAt section: Int) -> UIEdgeInsets {
            return UIEdgeInsets(top: 1, left: 0, bottom: 0, right: 0)
        }
        
        
# add customer cells (can be done in xib or storyboard)

 step1.   change 
 
        collectionView?.register(UICollectionViewCell.self, forCellWithReuseIdentifier: cellId)
        collectionView?.register(PhotoSelectorCell.self, forCellWithReuseIdentifier: cellId)
        
 step2.  add as! PhotoSelectorCell, this make cell a instance of PhotoSelectorCell instead of the generic  
         UICollectionViewCell and assign photoImageView to it
 
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: cellId, for: indexPath) as! PhotoSelectorCell
        cell.photoImageView.image = image[indexPath.item]


 *step0 photoSelectorCell (anchor is from an extesnion for UIView)
 
            class PhotoSelectorCell:UICollectionViewCell{
                let photoImageView: UIImageView = {
                    let iv = UIImageView()
                    iv.backgroundColor = .lightGray
                    return iv
                }()
                override init(frame: CGRect){
                    super.init(frame:frame)
                    addSubview(photoImageView)
                    photoImageView.anchor(top: topAnchor, left: leftAnchor, bottom: bottomAnchor, right: rightAnchor,
                    paddingTop:0, paddingLeft: 0, paddingBottom: 0, paddingRight: 0, width: 0, height: 0)
                }
                required init?(coder aDecoder: NSCoder) {
                    fatalError("init(coder:) has not been implemented")
                }
            }
            
            
# AspectFill (allow photo to have the right ratio..which means the picture can fall outside of the cell

        iv.contentMode = .scaleAspectFill //expand out side the bounds
        iv.clipsToBounds = true //cut the boarder

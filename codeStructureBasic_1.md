# Style I currently like

1) keep the declaration one line on top is easier to read
2) Separate Delegate, ViewSetup, define variables in separate extension with MARK: - to separate them 

# Style 1 - This way is easier to find what you need

 

                  class ViewController: UIViewController, UITextFieldDelegate {

                      var textfield0 =  UITextField()
                      var textfield1 =  UITextField()
                      var textfield2 =  UITextField()
                      var textfield3 =  UITextField()

                      override func viewDidLoad() {
                          super.viewDidLoad()
                          setupTextFields()
                      }

                  extension ViewController {
                      func setupTextFields(){
                          textfield0.delegate = self
                          textfield1.delegate = self
                          textfield2.delegate = self
                          textfield3.delegate = self

                          textfield0.tag = 0
                          textfield1.tag = 1
                          textfield2.tag = 2
                          textfield3.tag = 3

                          textfield0.borderStyle = .roundedRect
                          textfield1.borderStyle = .roundedRect
                          textfield2.borderStyle = .roundedRect
                          textfield3.borderStyle = .roundedRect

                          view.addSubview(textfield0)
                          view.addSubview(textfield1)
                          view.addSubview(textfield2)
                          view.addSubview(textfield3)

                          textfield0.anchor(top: topLayoutGuide.bottomAnchor, left: view.leftAnchor, bottom: nil, right: view.rightAnchor, paddingTop: 10, paddingLeft: 30, paddingBottom: 0, paddingRight: 30, width: 0, height: 30)

                          textfield1.anchorToTopView(viewOnTop: textfield0, paddingTop: 30)
                          textfield2.anchorToTopView(viewOnTop: textfield1, paddingTop: 30)
                          textfield3.anchorToTopView(viewOnTop: textfield2, paddingTop: 30)
                      }
                  }
                  
                  
# Style 2 - This way seems cool when I first learned about it but it doesn't make things easier

              class ViewController: UIViewController, UITextFieldDelegate {

                  lazy var textfield0:UITextField =  {
                      let tf = UITextField()
                      tf.delegate = self
                      tf.tag = 0
                      tf.borderStyle = .roundedRect
                      return tf
                  }()
                  lazy var textfield1:UITextField =  {
                      let tf = UITextField()
                      tf.delegate = self
                      tf.tag = 1
                      tf.borderStyle = .roundedRect
                      return tf
                  }()

                  lazy var textfield2:UITextField =  {
                      let tf = UITextField()
                      tf.delegate = self
                      tf.tag = 2
                      tf.borderStyle = .roundedRect
                      return tf
                  }()

                  lazy var textfield3:UITextField =  {
                      let tf = UITextField()
                      tf.delegate = self
                      tf.tag = 3
                      tf.borderStyle = .roundedRect
                      return tf
                  }()

                  override func viewDidLoad() {
                      super.viewDidLoad()
                      setupTextFields()
                  }
              }
              extension ViewController {
                  func setupTextFields(){
                      view.addSubview(textfield0)
                      view.addSubview(textfield1)
                      view.addSubview(textfield2)
                      view.addSubview(textfield3)

                      textfield0.anchor(top: topLayoutGuide.bottomAnchor, left: view.leftAnchor, bottom: nil, right: view.rightAnchor, paddingTop: 10, paddingLeft: 30, paddingBottom: 0, paddingRight: 30, width: 0, height: 30)

                      textfield1.anchorToTopView(viewOnTop: textfield0, paddingTop: 30)
                      textfield2.anchorToTopView(viewOnTop: textfield1, paddingTop: 30)
                      textfield3.anchorToTopView(viewOnTop: textfield2, paddingTop: 30)
                  }
              }



# Style 3 - Don't repeat your code... Not sure about this, sometimes is a good idea

              class ViewController: UIViewController, UITextFieldDelegate {

                  lazy var textfield:[UITextField] =  {
                      var tf = [UITextField]()
                      for i in 0...3 {
                          let t = UITextField()
                          t.delegate = self
                          t.tag = i
                          t.borderStyle = .roundedRect
                          tf.append(t)
                      }
                      return tf
                  }()
             //MARK: -
                  override func viewDidLoad() {
                      super.viewDidLoad()
                      setupTextFields()
                  }
              }
              //MARK: - Delegate Methods
              extension ViewController{
                  func textFieldDidEndEditing(_ textField: UITextField) {
                      //id currentfield by
                      //1. tag number
                      //2. compare textField to textField0,1,2..ect
                  }
              }
              //MARK: - View Setup
              extension ViewController {
                  func setupTextFields(){
                      view.addSubview(textfield[0])
                      view.addSubview(textfield[1])
                      view.addSubview(textfield[2])
                      view.addSubview(textfield[3])

                      textfield[0].anchor(top: topLayoutGuide.bottomAnchor, left: view.leftAnchor, bottom: nil, right: view.rightAnchor, paddingTop: 10, paddingLeft: 30, paddingBottom: 0, paddingRight: 30, width: 0, height: 30)

                      textfield[1].anchorToTopView(viewOnTop: textfield[0], paddingTop: 30)
                      textfield[2].anchorToTopView(viewOnTop: textfield[1], paddingTop: 30)
                      textfield[3].anchorToTopView(viewOnTop: textfield[2], paddingTop: 30)
                  }
              }



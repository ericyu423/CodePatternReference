

example 1.

        @objc class Person: NSObject {
            @objc dynamic var name = "old name"
        }
        let person = Person()

        person.observe(\Person.name, options: .old) { person, value in
            print("I am called \(person.name)")
            print("I was called \(String(describing: value.oldValue))")

        }
        person.name = "new name"
      
      
      
      
example 2.


          class CounterModel : NSObject {
              @objc dynamic var value = 10
              @objc dynamic var messages = [String]()
          }
          var model = CounterModel()

          model.observe(\CounterModel.value, options: [.initial]) { (model, change) in
              print("my value \(model.value)")
          }

          model.value = 11
          model.value = 12
          model.value = 13
          model.value = 16
          
          
          console:
          my value 10
          my value 11
          my value 12
          my value 13
          my value 16

exampe from apple:

                class MyObjectToObserve: NSObject {
                    @objc dynamic var myDate = NSDate(timeIntervalSince1970: 0) // 1970
                    func updateDate() {
                        myDate = myDate.addingTimeInterval(Double(2 << 30)) // Adds about 68 years.
                    }
                }
                class MyObserver: NSObject {
                    @objc var objectToObserve: MyObjectToObserve
                    var observation: NSKeyValueObservation?

                    init(object: MyObjectToObserve) {
                        objectToObserve = object
                        super.init()

                        observation = observe(
                            \.objectToObserve.myDate,
                            options: [.old, .new]
                        ) { object, change in
                            print("myDate changed from: \(change.oldValue!), updated to: \(change.newValue!)")
                        }
                    }
                }
                let observed = MyObjectToObserve()
                let observer = MyObserver(object: observed)
                observed.updateDate()
                
                
 example apple test:
 
                 import UIKit

                class ViewModel: NSObject {
                    @objc dynamic var myDate = "monday"
                    func updateDate() {
                        myDate = "tuesday"
                    }
                }
                class MyObserver: NSObject {
                    @objc var objectToObserve: ViewModel
                    var observation: NSKeyValueObservation?

                    init(object: ViewModel) {
                        objectToObserve = object
                        super.init()

                        observe(
                            \.objectToObserve.myDate,
                            options: [.old, .new]
                        ) { object, change in
                            print("myDate changed from: \(change.oldValue!), updated to: \(change.newValue!)")
                        }

                //        observation = observe(
                //            \.objectToObserve.myDate,
                //            options: [.old, .new]
                //        ) { object, change in
                //            print("myDate changed from: \(change.oldValue!), updated to: \(change.newValue!)")
                //        }
                    }
                }
                let observed = ViewModel()
                let observer = MyObserver(object: observed)
                observed.updateDate()
  example observe webpage loading
  
                import UIKit
                import WebKit

                class ViewController: UIViewController {

                    var seaWebView: WKWebView!
                    let keyPathToObserve:String = "estimatedProgress"
                    let urlString = "https://cnn.com"

                    override func viewDidLoad() {
                        super.viewDidLoad()
                        self.seaWebView = WKWebView()
                        self.view = seaWebView
                        self.seaWebView.addObserver(self, forKeyPath: keyPathToObserve, options: .new, context: nil)
                        loadPage()
                    }

                    func loadPage() {
                        guard let url = URL(string: urlString) else { return }
                        let urlRequest = URLRequest(url: url)
                        self.seaWebView.load(urlRequest)
                    }

                    override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {
                        if keyPath == keyPathToObserve {
                            print("Loaded \(self.seaWebView.estimatedProgress*100)%")
                        }
                    }

                    deinit {
                        self.seaWebView.removeObserver(self, forKeyPath: keyPathToObserve, context: nil)
                    }
                }

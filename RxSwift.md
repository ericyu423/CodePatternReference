* Another way to pass data without using Delegate Pattern

I. setup Cocopod setup
    pod 'RxSwift',    '~> 4.0'
    pod 'RxCocoa',    '~> 4.0'


        
        
# Detail View (user select data here and it will get pass back to the master view)
       
       private let selectedCharacterVariable = BehaviorRelay(value: "User")
       var selectedCharacter:Observable<String>{ return selectedCharacterVariable.asObservable()}


       your user action can call 
          selectedCharacterVariable.accept(
           "the string where you want to pass back to your main view controller"
          )
          
          
# Main View    

      @IBOutlet weak var myLabel: UILabel!
      let disposeBag = DisposeBag()  
      
      
      in the fucntion wher you  aregoing to your detail view controller
      
      let vc = storyboard?.instantiateViewController(withIdentifier: "DetailViewController") as! DetailViewController
        
        
        //basically this block get called wheneve selectedCharacter is changed
       vc.selectedCharacter.subscribe(onNext:{
            [weak self] x in
            self?.myLabel.text = "hello \(x)"
        }).disposed(by: disposeBag)

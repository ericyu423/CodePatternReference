 
    let formatter = DateFormatter()
    formatter.timeZone = TimeZone(abbreviation: "UTC")!
    formatter.dateFormat = "EEEE dd MMMM yyyy"
    
    
    let resultOfFormat = formatter.string(from: somedate)   //somedate: Date
    
    
    
    
    //interesting way to extend Date
    
    extend Date{
    
    func formatDate() -> String {
        return format(by: "EEEE dd MMMM yyyy") //some default format
    }
    
    
       func format(by format: String) -> String {
        let dateFormatter = DateFormatter()
        dateFormatter.timeZone = TimeZone(abbreviation: "UTC")!
        dateFormatter.dateFormat = format
        return dateFormatter.string(from: self)
    }
    }
    
    

        

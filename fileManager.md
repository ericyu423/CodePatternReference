
https://github.com/ericyu423/FileManger



# book object

        class Book: NSObject, NSCoding {
            var title: String?
            var author: String?
            var edition: Int?

            init(btitle: String, bauthor: String, bedition:Int){
                title = btitle
                author = bauthor
                edition = bedition
            }
            func encode(with aCoder: NSCoder) {
                aCoder.encode(title, forKey: "title")
                aCoder.encode(author, forKey: "author")

                //problem with saving stuff in Int whatever taking me too much time
                //saving as anyobject and coverted back is the same
                aCoder.encode(edition!, forKey: "edition")

            }
            required init?(coder aDecoder: NSCoder) {
                title =   aDecoder.decodeObject(forKey: "title") as? String
                author =  aDecoder.decodeObject(forKey: "author") as? String
                edition = aDecoder.decodeObject(forKey: "edition") as? Int
            }
        }



//this saves 

   func saveBook(book: Book){
        let manager = FileManager.default
        let document = manager.urls(for: .documentDirectory, in: .userDomainMask)
        let docURL = document.first!
        let fileURL = docURL.appendingPathComponent("book.dat")
        let filePath = fileURL.path
        let fileData = NSKeyedArchiver.archivedData(withRootObject: book)
            manager.createFile(atPath: filePath, contents: fileData, attributes: nil)

    }
    
    
    func loadFile(){
        //get file pathfrom bundle (FileManager bundle)
        let filePath = Bundle.main.path(forResource: "mySpeicalFile", ofType: "txt")
        let manager = FileManager.default
        if let filePath = filePath,let data = manager.contents(atPath: filePath){
            let message = String(data: data, encoding: .utf8)
            fileTextView.text = message
        }else{
            print("file not found")
        }
    }
    
    
    
//appDelegate

   func getDocURL() ->(URL,FileManager) {  //think of it as a way to find your direcotry in temrinal
        let manager = FileManager.default //Returns the shared file manager object for the process.
        let documents = manager.urls(for: .documentDirectory, in: .userDomainMask)
        let docURL = documents.first! //only one .documentDirectory so is save to unwarp
        return (docURL,manager)
        
        
        //create a default file manager
        //ask file manager to return .documentDirectory url ...pwd
        //since it return an array for .documentDiretory of our app there will only be one
        //so documents.first
        
        
        //docURL = //Users/ericyu423/Library/Developer/CoreSimulator/
        //         Devices/B84F70DF-E63E-470C-884C-85F5A4F8C4C4/data/
        //         Containers/Data/Application/F9F57530-3593-4607-B85C-408447283C76/Documents/
    }
    
    func createFile(docURL:URL,manager: FileManager){// think of it as "touch" unix command
        let newFileURL = docURL.appendingPathComponent("mytext.txt") //add something inside the folder
        let path = newFileURL.path  //docURL/mytext.txt"
        manager.createFile(atPath: path, contents: nil, attributes: nil)
        
        //seem to me this hold docURL appedning is helping you to do
        //docUR.append("'/'mytext.txt")
    }
    
    func createDirectory(docURL:URL,manager: FileManager){ //same as mkdir
         let newDirectoryURL = docURL.appendingPathComponent("MyStash", isDirectory: true)
         let path = newDirectoryURL.path
         do {
            try manager.createDirectory(atPath: path, withIntermediateDirectories: false, attributes: nil)
         }catch{
            print("failed to create new directory for file")
        }
    }
    
    func listItems(docURL:URL,manager: FileManager){//ls, dir
    
         let listItems = try? manager.contentsOfDirectory(atPath: docURL.path)
         if let list = listItems { //if stuff inside list it
            if list.isEmpty {
                print("the Directory is empty")
            }else {
                for item in list {
                    
                    print(item)
                    
                    listDirectoryInsideList(docURL: docURL,manager: manager, item: item)
                }
            }
         }
    }
    func listDirectoryInsideList(docURL:URL,manager: FileManager,item:String){
        let newDirectoryURLpath = docURL.appendingPathComponent(item, isDirectory: true).path
     
            let listItems = try? manager.contentsOfDirectory(atPath: newDirectoryURLpath)
            if let list = listItems { //if stuff inside list it
                if list.isEmpty {
                    print("sub Directory is empty")
                }else {
                    for item in list {
                        
                        print(item)
                        print("\(newDirectoryURLpath)\(item)")
                        
                        ///Users/ericyu423/Library/Developer/CoreSimulator/Devices/B84F70DF-E63E-470C-884C-85F5A4F8C4C4/data/Containers/Data/Application/A2F4AB25-3229-4E66-80B8-AE6DCA914343/Documents/MyStashmytext.txt
                    }
                }
            }
    }
    
    func moveDirectory(docURL: URL,manager:FileManager){
        let currentFileURL = docURL.appendingPathComponent("mytext.txt")
        let newDirURL = docURL.appendingPathComponent("MyStash/mytext.txt", isDirectory: true)
        ///don't need to convert to path
        //moveItem takes both path and just pure ULR
        do {
            try manager.moveItem(at: currentFileURL, to: newDirURL)
            print("moving file success")
        }catch{
            print("failed moving file")
        }

    }
    func removeFile(docURL: URL,manager:FileManager){
        //probably want the fuction that takes the name too
        //fileName: String
        
        //well we do need to know where exactly it is
        //if you are sure is under docULR/mytext.txt than it will work
        let fileURL = docURL.appendingPathComponent("mytext.txt")
        
        do{
            try manager.removeItem(at: fileURL)
        }catch{
            print("file was not removed")
        }
    }
    
    func getFileAttribute(docURL: URL,manager:FileManager){
        
        var fileURL = docURL.appendingPathComponent("mystash")
        fileURL = docURL.appendingPathComponent("mytext.txt")
        // this is like cd mystash, cd mytext.txt
        
        if let attribute = try? manager.attributesOfItem(atPath:fileURL.path){
           
            let type = attribute[.type] as! String
            let size = attribute[.size] as! Int
            let date = attribute[.creationDate] as! NSDate
            let directoryType = FileAttributeType.typeDirectory.rawValue
           
            print(directoryType) // "NSFileTypeDirectory"
            if type != directoryType{
                
                print("Name: \(fileURL.lastPathComponent)")
                print("Size: \(size)")
                print("Created: \(date)")
                
            }
                /*Name: mytext.txt
                 Size: 0
                 Created: 2017-11-05 07:03:29 +0000*/
            
            
        }
        
        
    }
    
    
    func copyFile(docURL: URL,manager:FileManager){
        let originURL = docURL.appendingPathComponent("mytext.txt") // /Documents/MyStash/mytext.txt
        let newDirURL = docURL.appendingPathComponent("MyStash/mytext.txt")  ///Documents/mytext.txt
        
        do {
            try manager.copyItem(at: originURL, to: newDirURL)
        }catch{
            print("failed moving file")
        }
    }
    

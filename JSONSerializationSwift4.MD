read more details: https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types

# JSON -> Struct simple case

                struct Traveler: Decodable {
                    let fullName: String
                    let id: Int
                    let web: URL
                }

                let json = """
                {
                 "fullName": "a",
                 "id": 1,
                 "web": "http://google.com"
                }
                """

                 let data = json.data(using: .utf8)! //if it came in as data you won't need to convert it
                 let traveler = try JSONDecoder().decode(Traveler.self, from: data)


                print(traveler)
                
# If is an array

          let traveler:[traveler] = try JSONDecoder().decode([Traveler].self, from: data)
          
# If is an dictionary

          let traveler:[String:Traveler] = try JSONDecoder().decode([String: Traveler].self, from: json)

          traveler.forEach { print("\($0.key): \($0.value)") } //print it out to see
          
          

# Enum (from https://stackoverflow.com/questions/44580719/how-do-i-make-an-enum-decodable-in-swift-4)

                      enum PostType : Int, Codable {
                    case count = 4
                }

                struct Post : Codable {
                    var type : PostType
                }

                let jsonString = "{\"type\": 4}"

                let jsonData = jsonString.data(using: .utf8)!

                do {
                    let decoded = try JSONDecoder().decode(Post.self, from: jsonData)
                    print("decoded:", decoded.type)
                } catch {
                    print(error)
                }



# JSON response *more examples*

        {
          name: "My Swift Course"
          description: "Fast learning"
          courses: [
            {
                id: 1,
                name: "eric yu",
                link: "https://somethingsomethinglink",
                imageUrl: "https://somethingsomething.jpg"
            }
            {
                id: 2,
                name: "eric yu2",
                link: "https://somethingsomethinglink",
                imageUrl: "https://somethingsomething.jpg"
            }
          ]
        }
        
# Swift4 (turning it into one of your swift object with structure)

step 1. contruct model object bottom up, also make it "comform" to Decodable protocol you do not need an init

            {
                id: 2,
                name: "eric yu2",
                link: "https://somethingsomethinglink",
                imageUrl: "https://somethingsomething.jpg"
            }
 -----------------------------------------------------------------------------             
         
         struct Course {
              let id: Int
              let name: String
              let link: String
              let imageUrl: String
          }
-----------------------------------------------------------------------------          
          
          {
             name: "My Swift Course"
             description: "Fast learning"
             courses: [ ]
           }
-----------------------------------------------------------------------------    
          
          struct Subject: Decodable {
                let name: String
                let description: String
                 let courses: [Course]  //course is an array of struct Course ojb
          
          }
          
          
 step 2. function to populate your model
 
        // call the function in viewDidLoad or when you press a button or something

        func compoundinSwift4(){
            let jsonUrlString = "https://placewhereyougetyourInformationInJason" 
            //without http"s" you will need to modified trasnport security in polist else u get an error
            guard let url = URL(string: jsonUrlString) else {return}

            URLSession.shared.dataTask(with: url)
            { (data,reponse, err) in

                guard let data = data else {return}
                do{
                    let course = try JSONDecoder().decode(Subject.self, from: data)

                }catch let error {
                    print("Error serializaing json:", error)
                }
                }.resume()

        }
        
        
        
          


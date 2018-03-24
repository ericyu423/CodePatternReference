# frequently used

# unless you are creating 2 classes in a same file and want them to share a function and no one else there is no point for fileprivate

            //file 1.swift
            extension ViewController {
                func start3(){
                    print(myfileprivate) //works same file
                    print(myprivate)  //works 
                    print(myregular) //works
                }
            }

            class test {

                var vc = ViewController()
                func start(){
                    vc.myinternal()//no
                    vc.mytest()//private functon doesn't work
                    vc.setupInputFields()//fileprivate works, a private within the same file
                }
            }
            
            
            
            
            
            //file 2.swift
            class test2 {
                var vc = ViewController()
                func start(){
                   vc.myinternal()//regular (internal) acess
                   vc.mytest()//private obviously won't work
                   vc.setupInputFields()//fileprivate don't work
                }
            }

          extension ViewController {

              func test5(){
              print(myfileprivate)//extension but different file won't work
              print(myprivate)//extension wont' work
              print(myregular)
              }

          }

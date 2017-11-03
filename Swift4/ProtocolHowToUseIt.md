
# how to use protocol

They basically are reverse classes and easier to use.

so "super class" is the Fruit and Pen, they are the category

apple and pineapple are two things

(things): Fruit
(things): Fruit, Pen

while class give the varable to you to use
in protocol you just write them out and impliement it
if you want to "inherit" from the protocol
use


extension Fruit where Self:Pen


Questions unanswered:struct Apple Fruit,pen get your an error
if we change
      struct Apple: Fruit {
          var color: UIColor {
              return .red
          }

          func draw(){

          }

      }

error: MyPlayground.playground:96:14: error: type 'Apple' does not conform to protocol 'Pen'
print(fruit2.canBecomeViral)





      protocol Fruit {
          var color: UIColor {get}  //need to get a color
          var canBecomeViral: Bool { get}
      }


      protocol Pen{
          func draw()
      }

      extension Fruit where Self:Pen {
          var canBecomeViral: Bool {return true}
      }
      struct Appe: Fruit,Pen {
          var color: UIColor {
              return .red
          }

          func draw(){

          }

      }

      struct Pineapple: Fruit,Pen {
         var color = UIColor.red
          func draw() {
          }

      }
      let fruit = Pineapple()
      print(fruit.canBecomeViral)

source: https://www.youtube.com/watch?v=lBr8onqP_fM


// in class it be soemthing like this, you can't even inherit 2 classes

class Fruit {
    var color:UIColor!
    var canBecomeViral = true
}

class Pen {
    func draw(){
        //return nothing
    }
}
class Apple: Fruit {
  
  
}

#  StackView 

      let stackView: UIStackView = {
            let sv = UIStackView()
            sv.translatesAutoresizingMaskIntoConstraints = false
            sv.distribution = .fillEqually
            sv.axis = .horizontal
            sv.spacing = 25
            sv.backgroundColor = .red 
           return sv
      }()


#  StackView  stackView array

        let stackView: [UIStackView] = {
                var sv = [UIStackView]()
                for i in 0...2 {
                    let stackView = UIStackView()
                    s.translatesAutoresizingMaskIntoConstraints = false
                    s.distribution = .fillEqually
                    s.axis = .horizontal
                    s.spacing = 25
                    s.backgroundColor = .red
                    sv.append(s)
                }
                return sv
           }()
           
           
#  put views in stack

            boardView.addSubview(stackView[0])
            boardView.addSubview(stackView[1])
            boardView.addSubview(stackView[2])

            for i in 0...2 {
                for j in 0...2 {
                    stackView[i].addArrangedSubview(pView[j + (i * 3)])
                }  //(0,0),(0,1),(0,2),(1,3),(1,4),(1,5)...(2,8)
            }

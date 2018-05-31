Just have a variable inside the draw that we can manipulate.

Note: this is like subclassing a Switch or Slider



class ViewController: UIViewController, LogoTraceDelegate {

    @IBOutlet weak var statusLabel: UILabel!
    @IBOutlet weak var traceView: LogoView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        traceView.delegate = self
    }

    
    func logoTraceComplete() {
        statusLabel.text = "Trace complete"
    }
    
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }


}


protocol LogoTraceDelegate {
    func logoTraceComplete()
}

@IBDesignable
class LogoView: UIView {
    
    var yPositionPercentage:CGFloat = 0
    var traceCompleted = false
    
    var delegate:LogoTraceDelegate?
   
    override func draw(_ rect: CGRect) {
    
        let context = UIGraphicsGetCurrentContext()!

        let color = UIColor(red: 0.882, green: 0.882, blue: 0.851, alpha: 1.000)
        let gradientColor = UIColor(red: 0.157, green: 0.169, blue: 0.208, alpha: 1.000)
        let gradientColor3 = UIColor(red: 0.498, green: 0.498, blue: 0.620, alpha: 1.000)
  
        let gradient = CGGradient(colorsSpace: nil, colors: [gradientColor.cgColor, gradientColor3.cgColor] as CFArray, locations: [0, 1])!
        
        //// Rectangle Drawing
        let rectanglePath = UIBezierPath(rect: CGRect(x: 1, y: 1, width: 63, height: 213))
        context.saveGState()
        rectanglePath.addClip()
        context.drawLinearGradient(gradient, start: CGPoint(x: 32.5, y: 1), end: CGPoint(x: 32.5, y: self.frame.height * yPositionPercentage), options: [])
        context.restoreGState()
        color.setStroke()
        rectanglePath.lineWidth = 1
        rectanglePath.stroke()

    }
    
    
    override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {
        if let touchPoint = touches.first?.location(in: self) {
            yPositionPercentage = touchPoint.y / self.frame.size.height
            updateDrawing()
        }
    }
    
    
    override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {
        updateDrawing()
        if yPositionPercentage >= 1 {
            traceCompleted = true
            if delegate != nil {
                delegate?.logoTraceComplete()
            }
        }
    }
    func updateDrawing () {
        
        if !traceCompleted {
            if yPositionPercentage > 0 && yPositionPercentage < 1 {
                self.setNeedsDisplay()
            }
        }
    }
}



source: https://www.youtube.com/watch?v=5KXtbkP49Z8

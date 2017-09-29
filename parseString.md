






"aasfadsf/lkjk/".slice(from:"/",to"/") give you optional(lkjk)
extension String {  
    func slice(from: String, to: String) -> String? {
        
        return (range(of: from)?.upperBound).flatMap { substringFrom in
            (range(of: to, range: substringFrom..<endIndex)?.lowerBound).map { substringTo in
                String(self[substringFrom..<substringTo])
            }
        }
    }
}









"2+4" //it doesn't throw errors so make sure is a good expression
let expression = NSExpression(format: mathExpression)
let result = expression.expressionValue(with: nil, context: nil) as! NSNumber

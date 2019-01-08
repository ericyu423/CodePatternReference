let missingKey = "key is missing - not a null value, is the key that is missing which should not happen"

class Bill: NSObject, Codable
{

    let title, inactiveText, category: SomeType
    let state: String
    let billDetails, billDetailsSubtext: SomeType?


    
    required init(from decoder: Decoder) throws {
        let container = try decoder.container(keyedBy: CodingKeys.self)
        self.title = try container.decodeIfPresent(SomeType.self, forKey: .title) ?? SomeType(string: missingKey, htmlIncluded: false)
        self.state  = try container.decodeIfPresent(String.self, forKey: .state) ?? missingKey
        self.icon  = try container.decodeIfPresent(String.self, forKey: .icon) ?? missingKey
    }
}

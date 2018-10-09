import UIKit

public class Someclass: NSObject
{
    private let queue: DispatchQueue
    var cachedItems: NSMutableArray = NSMutableArray()

    public init(fileName: String)
    {
        cacheFileName = fileName
        queue = DispatchQueue(label: "com.whatever.cocurrentQueue", attributes: .concurrent)
    }
  
    public func addToCache
    {
        queue.async(flags: .barrier)
        {
            self.cachedItems.addObjects(from: item)
        }
    }
    
    public func removeFromCache
    {
        queue.async(flags: .barrier)
        {
            self.cachedItems.remove(item)
        }
    }

}

barrier lock it till is done
http://basememara.com/creating-thread-safe-arrays-in-swift/







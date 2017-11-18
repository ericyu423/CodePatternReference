# Using -  if let (statement),(statement) { return }

- sometimes it makes it easier to read, but not all the time


          static func tripStatusEditability(status: String? ,endDate: Date?) -> Bool {
            var isPastTrip = true
          /* if let endDate = endDate {
              if endDate > Date() {
                  isPastTrip = false
              }else {
                  isPastTrip = true
              }
          }*/

          if let endDate = endDate, endDate > Date()
          {
              isPastTrip = false

          }

          if isPastTrip { return false}


          if let status = status, status.caseInsensitiveCompare("confirmed") != .orderedSame {return false}

          /*
          if let status = status {
              if status.caseInsensitiveCompare("confirmed") != ComparisonResult.orderedSame || isPastTrip {
                  return false
              }
          }
          guard status != nil else {
              return false
          }*/

          return true
      }

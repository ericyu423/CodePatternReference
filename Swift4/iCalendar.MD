# Incomplete file will need to be modified   
    
    
    import EventKit
     
     let eventStore = EKEventStore()
     
      func checkEventStoreAccessForCalendar(){
        let status = EKEventStore.authorizationStatus(for: .event)
        if(status == .notDetermined){
            requestCalendarAccess()
        }
    }
    
    
     func requestCalendarAccess(){
        eventStore.requestAccess(to: .event) { granted, error in
            if (granted){
                print("Access Granted to Calendar ...")
            }
        }
    }
    
    
     func addEvent(_ newItem: NewItem){
        
        let calendarForEvent = eventStore.defaultCalendarForNewEvents
        
        let newEvent = EKEvent(eventStore: eventStore)
        
        newEvent.calendar = _
        newEvent.title = _
        newEvent.notes = _
        newEvent.location = _
        newEvent.startDate = _
        newEvent.endDate = _
        
        var tripQuery = ""
        if let code = destinationHandler?.currentTrip?.reservationCode,
            let escapedName = code.addingPercentEncoding(withAllowedCharacters: .urlHostAllowed) {
            tripQuery = "&trip=\(escapedName)"
        }
        let timeQuery = Int64(excursion.timeSlot.start.timeIntervalSince1970)
        newEvent.url = URL(string: "\(ApplicationURLScheme)?q=\(timeQuery)\(tripQuery)")
        
        // Save the calendar using the Event Store instance
        
        do {
            try eventStore.save(newEvent, span: .thisEvent, commit: true)
            dismiss(animated: true, completion: nil);
        } catch {
            print("event couldn't be saved \(error.localizedDescription)")
        }
    }

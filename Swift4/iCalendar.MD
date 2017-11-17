# read/write to ical 
    
# Issues

* if the source is icloud once you write it, the user can not delete it from iphone



* it can only be delete from the icloud account


# issue with icloud (add this check)


             func getSource() -> EKSource? {
                 if let defaultSource = eventStore.defaultCalendarForNewEvents?.source {
                     //may have iCloud account, and then we will not have a local source
          
                 return defaultSource
             }

             if let localSource = eventStore.sources.first(where: { $0.sourceType == .local }) {
           
                 areturn localSource
             }
             return nil
         }



    import Foundation
    import EventKit

    class EventWriter {
    
    var eventStore = EKEventStore()

    func createNewCalendarWithID(reservationCode code: String)->String{
        
        removeCalendar(withReservationCode: code)
        
        let newCalendar = EKCalendar(for: .event, eventStore: eventStore)
        newCalendar.title = "Trip( "+code+" )"
        
        let filteredSources = eventStore.sources.filter {
            $0.sourceType == .local }
        
        if let localSource = filteredSources.first {
            
            newCalendar.source = localSource
            
            do {
                try eventStore.saveCalendar(newCalendar, commit: true)
                UserDefaults.standard.set(newCalendar.calendarIdentifier,forKey:code)
                print("succesfully save calendar with id"+newCalendar.calendarIdentifier)
                
            } catch {
                print("save failed\(error.localizedDescription)")
            }
            
        }else{
            print("no local source found")
        }
        
        return newCalendar.calendarIdentifier
    }
    
    func checkEventStoreAccessForCalendar(){
        
        let status = EKEventStore.authorizationStatus(for: .event)
        if(status == .notDetermined){
            requestCalendarAccess()
        }
    }
    
    func addEvent(calendarID: String?,title: String){
        

        let calendars = eventStore.calendars(for: .event).filter {
            $0.calendarIdentifier == calendarID
            }
        
        if let calendarForThisEvent = calendars.first {
        
        
        let newEvent:EKEvent = EKEvent(eventStore: eventStore)
        
        newEvent.calendar = calendarForThisEvent
        newEvent.title = title
        newEvent.startDate = Date()
        newEvent.endDate = Date()
            
        
        /*
         var tripQuery = ""
         if let code = destinationHandler?.currentTrip?.reservationCode,
         let escapedName = code.addingPercentEncoding(withAllowedCharacters: .urlHostAllowed) {
         tripQuery = "&trip=\(escapedName)"
         }*/
        /* let timeQuery = Int64(excursion.timeSlot.start.timeIntervalSince1970)
         newEvent.url = URL(string: "\(ApplicationURLScheme)?q=\(timeQuery)\(tripQuery)")*/
        
        // Save the calendar using the Event Store instance
        
            do {
                try eventStore.save(newEvent, span: .thisEvent, commit: true)
            } catch {
                print("event couldn't be saved \(error.localizedDescription)")
            }
        }
  
        
    }

}

    extension EventWriter {
    private func requestCalendarAccess(){
        eventStore.requestAccess(to: .event) { (granted, error) in
            if granted{
                print("Access Granted to Calendar ...")
                //get rid of warnning
            }
        }
    }
    
    private func removeCalendar(withReservationCode code : String){
        
        if let calendarID = UserDefaults.standard.value(forKey: code) as? String {
            
            /* eventStore.calendar(withIdentifier: calendarID) gaves types 3 from daemon: Error Domain=EKCADErrorDomain Code=1014 */
            let calendars = eventStore.calendars(for: .event).filter{
                $0.calendarIdentifier == calendarID
            }
            
            if let newCalendar = calendars.first {
                do {
                    try eventStore.removeCalendar(newCalendar, commit: true)
                    print("succesfully removed "+code)
                }catch{
                    print("calendar can't be removed \(error.localizedDescription)")
                }
            }
            
        }
    }
    
}

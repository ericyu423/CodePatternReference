    table cell selected this will unselected also prevent divider line from disappearing 
    
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)
    {
            tableView.deselectRow(at: indexPath, animated: true) 
    }

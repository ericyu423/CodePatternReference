 fileprivate func setupTableFooter()
    {
        let disclosureText = "*See View Details & Disclosures for more information."
        let labelLeftSpacing: CGFloat = 20
        let labelTopSpacing: CGFloat = 5
        let footerViewHeight: CGFloat = 50
        
        let footerView = UIView(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: footerViewHeight))
        
        let footerViewLabel: UILabel =
        {
            let label = UILabel()
            label.numberOfLines = 1
            label.font = EWFontController.sharedInstance.font(forTextStyle: EWTextStyle.kBody2Regular)
            label.textColor = UIColor.experianWorksTextDarkGray1()
            label.textAlignment = .left
            label.minimumScaleFactor = 0.5
            label.adjustsFontSizeToFitWidth = true
            label.translatesAutoresizingMaskIntoConstraints = false
            label.text  = disclosureText
            return label
        }()
        
        footerView.addSubview(footerViewLabel)

        footerViewLabel.topAnchor.constraint(equalTo: footerView.topAnchor, constant: labelTopSpacing).isActive = true
        footerViewLabel.bottomAnchor.constraint(equalTo: footerView.bottomAnchor, constant: 0 ).isActive = true
        footerViewLabel.leftAnchor.constraint(equalTo: footerView.leftAnchor, constant: labelLeftSpacing).isActive = true
        footerViewLabel.rightAnchor.constraint(equalTo: footerView.rightAnchor, constant: 0).isActive = true
       
        tableView.tableFooterView = footerView
    }

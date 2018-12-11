func addShadowGradian(toView v: UIView)
    {
        v.layer.shadowColor     = UIColor.white.cgColor
        v.layer.masksToBounds = false;
        v.layer.shadowRadius    = 7;
        v.layer.shadowOpacity   = 1;
        v.layer.shadowPath      = UIBezierPath(rect: v.bounds).cgPath
    }

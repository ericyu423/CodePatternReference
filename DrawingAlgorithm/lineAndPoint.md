        Given end points (x1,y1) (x2,y2)  , item midePoint at (x3,y3)

        find penpendicular intercept point on linle (x4,y4)


//reference from https://stackoverflow.com/questions/1811549/perpendicular-on-a-line-from-a-given-point

        double dx = x2 - x1;
        double dy = y2 - y1;
        double mag = sqrt(dx*dx + dy*dy);
        dx /= mag;
        dy /= mag;

        // translate the point and get the dot product
        double lambda = (dx * (x3 - x1)) + (dy * (y3 - y1));
        x4 = (dx * lambda) + x1;
        y4 = (dy * lambda) + y1;

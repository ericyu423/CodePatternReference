source: https://stackoverflow.com/questions/20388427/compress-uiimage

calculator https://toolstud.io/photo/megapixel.php?width=750&height=750&compare=video&calculate=uncompressed

500x500 = 250000 
250000/1000 = 250k


    - (UIImage *)scaleImage:(UIImage *)image toSize:(CGSize)newSize {
        CGSize actSize = image.size;
        float scale = actSize.width/actSize.height;

        if (scale < 1) {
            newSize.height = newSize.width/scale;
        } else {
            newSize.width = newSize.height*scale;
        }


        UIGraphicsBeginImageContext(newSize);
        [image drawInRect:CGRectMake(0, 0, newSize.width, newSize.height)];
        UIImage* newImage = UIGraphicsGetImageFromCurrentImageContext();
        UIGraphicsEndImageContext();

        return newImage;
    }
    
[self scaleImage:yourUIImage toSize:CGMakeSize(300,300)];    

custom error message

msg, error code and errorDomain can be anything you want


apiError = [NSError errorWithDomain:@"com.addID.appName" code:0 userInfo:[NSDictionary dictionaryWithObject:msg forKey:NSLocalizedDescriptionKey]];

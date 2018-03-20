
I don't know why I never encounter, or I have and just forgot but this problem is quit annoying

so basically create a Set because repeating items
and go throught the loop while record the index that you should be taken out first


                  NSMutableIndexSet *discardedItems = [NSMutableIndexSet indexSet];
                  NSMutableArray *allData = [App getInstance].measureHistory;
                  NSUInteger index = 0;

                  NSString * historyToClear = [[NSUserDefaults standardUserDefaults] objectForKey:KEEPHISTORYOPTIONKEY];

                  for(LASMeasurement *measure in allData) {

                      NSLog(@"%@", historyToClear);
                      if ([historyToClear isEqualToString: @"noted"] && ![measure.note isEqual: @""]){
                          [discardedItems addIndex:index];
                      }else if ([historyToClear isEqualToString: @"allExceptNoted"] && [measure.note isEqual: @""]){
                          [discardedItems addIndex:index];
                      }else if ([historyToClear isEqualToString: @"allHistory"]){
                          [discardedItems addIndex:index];
                      }

                  }

                  [[App getInstance].measureHistory removeObjectsAtIndexes:discardedItems];
                  [[App getInstance] saveMeasureHistory];


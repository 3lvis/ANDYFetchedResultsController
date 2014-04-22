ANDYFetchedResultsController
============================

The idea is to write this:

```objc
NSFetchedResultsController *fetchedResultsController = [[[[Midget fetchInContext:context]
                                                                           where:@"type == 'abc'"]
                                                                          sortBy:@"createdDate"]
                                                                           limit:5];
NSError *error = nil;
if (![self.fetchedResultsController performFetch:&error]) {
  // handle error
}
```

Instead of this:

```objc
NSFetchRequest *fetchRequest = [[NSFetchRequest alloc] init];
NSEntityDescription* entity = [NSEntityDescription entityForName:@"Midget" 
                                          inManagedObjectContext:context];
[fetchRequest setEntity:entity];

NSPredicate *predicate = [NSPredicate predicateWithFormat:@"type == 'abc'"];
[fetchRequest setPredicate:predicate];

NSSortDescriptor *sortDescriptor = [[NSSortDescriptor alloc] initWithKey:@"createDdate" 
                                                               ascending:YES];

NSArray *sortDescriptors = [[NSArray alloc] initWithObjects:sortDescriptor, nil];
[fetchRequest setSortDescriptors:sortDescriptors];
[fetchRequest setFetchLimit:5];

NSFetchedResultsController *fetchedResultsController = [[NSFetchedResultsController alloc] initWithFetchRequest:fetchRequest 
                                                                                           managedObjectContext:context 
                                                                                             sectionNameKeyPath:nil
                                                                                                      cacheName:nil];

NSError *error = nil;
if (![self.fetchedResultsController performFetch:&error]) {
  // handle error
}
```

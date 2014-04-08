ANDYFetchedResultsController
============================

Write this:

```objc
NSFetchedResultsController *fetchedResultsController = [[[[Widget fetchInContext:context]
                                                                           where:@"type == 'abc'"]
                                                                          sortBy:@"createdDate"]
                                                                           limit:5];
NSError *error = nil;
if (![self.fetchedResultsController performFetch:&error]) {
  // print error
}
```

Instead of this:

```objc
NSFetchRequest* fetchRequest = [[NSFetchRequest alloc] init];
NSEntityDescription* entity = [NSEntityDescription entityForName:@"Widget" inManagedObjectContext:self.managedObjectContext];
[fetchRequest setEntity:entity];

NSPredicate* predicate = [NSPredicate predicateWithFormat: @"type == 'abc'"];
[fetchRequest setPredicate:predicate];

NSSortDescriptor* sortDescriptor = [[NSSortDescriptor alloc] initWithKey:@"createDdate" ascending:YES];

NSArray* sortDescriptors = [[NSArray alloc] initWithObjects: sortDescriptor, nil];
[fetchRequest setSortDescriptors:sortDescriptors];
[fetchRequest setFetchLimit:5];

NSFetchedResultsController *fetchedResultsController = [[NSFetchedResultsController alloc] initWithFetchRequest:fetchRequest managedObjectContext:context sectionNameKeyPath:nil cacheName:nil];

NSError *error = nil;
if (![self.fetchedResultsController performFetch:&error]) {
  // print error
}
```

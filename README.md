ANDYFetchedResultsController
============================

The idea is to write this:

```swift
let fetchedResultsController = Midged.fetch(context).where("type == 'abc'").sortBy("createdDate").limit(5)
fetchedResultsController.performFetch(nil)
```

Instead of this:

```swift
let fetchRequest = NSFetchRequest()
fetchRequest.entity = NSEntityDescription(name: "Midged", managedObjectContext:context)
fetchRequest.predicate = NSPredicate(format: "type == 'abc'")

let sortDescriptor = NSSortDescriptor(key: "createDate", ascending: true)
fetchRequest.sortDescriptors = [sortDescriptor]
fetchRequest.fetchLimit = 5

let fetchedResultsController = NSFetchedResultsController(fetchRequest: fetchRequest, managedObjectContext: context, sectionNameKeyPath: nil, cacheName: nil)
fetchedResultsController.performFetch(nil)
```

## Formatting and Style

1.	Lines should be no longer than 120 charactes long for easy readability  

2.	Remove ```Using``` statement that aren’t actually referenced in the file and organize it by right clicking on namespace -> Remove and Sort Using. 

3. Use ```Using``` only for the following types e.g.:
```cs
System.Collections.Generic.IEnumerable<> 
```

If Class is internal then give full name of the class or the service:
```cs
EF.Document document = _entities.Document.SingleOrDefault(item => item.ID == documentId);
```
OR
```cs
private readonly Services.Document _documentService;
 ````
4.	Do not indent object intializers and initialize each property on a new line: 

Instead of this:
```cs
IEnumerable<Customer> customers = dbCustomers.Select(customer => new Customer { Name = customer.Name, Address = customer.Address, Number = customer.Number });
```
Do this:
```cs
IEnumerable<Customer> customers = dbCustomers.Select(customer => new Customer
{
    Name = customer.Name,
    Address = customer.Address,
    Number = customer.Number
}); 
```
5.	Omit extra blank lines in a method. 

6.	When using LINQ, separate lines by LINQ function for easy readibility. 

Instead of this:
```cs
var missingArrivalTimes = tripDays.Where(item => item.Date >= currentSurvey.DateStart && item.Date <= currentSurvey.DateEnd).Any(tripDay => tripDay.Trips.OrderBy(trip => trip.Ordinal).First().TripMode.RequiresTime && !tripDay.TimeArrived.HasValue);
```
Do this:
```cs
var missingArrivalTimes = tripDays
	.Where(item => item.Date >= currentSurvey.DateStart && item.Date <= currentSurvey.DateEnd)
	.Any(tripDay => tripDay.Trips
	.OrderBy(trip => trip.Ordinal)
	.First().TripMode.RequiresTime && !tripDay.TimeArrived.HasValue);
```
7. Instead of writing ```.ToList().ForEach()``` 
```cs
templateEntity.PlanetBidTemplatePriceSections
	.ToList()
	.ForEach(item => CreateStorage(item, entity));
```

Refactor it to ```foreach``` loop
```cs
foreach (var templatePriceSection in templateEntity.PlanetBidTemplatePriceSections)
{
	var priceSection = CreatePriceSection(templatePriceSection, planetBidEntity.ID);
	planetBidEntity.PlanetBidPriceSections.Add(priceSection);
}
```

## Naming

1. Service class should have method names as Verbs
2. Controller should have method names as Nouns
3. Do not use abbreviation, give a descriptive name to variables, methods, classes and etc.

## Maintainability

1. Do not declare a variable if it is not used anywhere

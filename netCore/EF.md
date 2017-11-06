# EF

1. 关于 DBFunction 的问题

``` cs
 var result = from c in _context.Dice
       group c by c.EventTime.Date into grp
       select new DailyDiceViewModel
       {
           EventTime = grp.Key,
           DiceCount = grp.Count(),
           Amount = grp.Sum(x => x.Amount),
           PrizeCount = grp.Where(
               x => !(_context.Prize.Where(_ => _.Reserved==true)
               .Select(c=> c.PrizeID))
               .Contains(x.PrizeID)
               ).Count()   
       };
```

2. 关于FluentAPI hasColumnName 的问题
需要引用 Microsoft.EntityFrameworkCore.Relational
```
install-package Microsoft.EntityFrameworkCore.Relational
```

代码中，可以看到 EF Core 支持对时间字段 ```c.EventTime``` 取属性 ```Date```，得到只包含日期的字段，用于分组。

## 参考资料
1. [EF Core for Enterprise](https://www.codeproject.com/Articles/1160586/EF-Core-for-Enterprise)

2. [Learn Entity Framework Core](http://www.learnentityframeworkcore.com/)

3.  [Architecture of Business Layer working with Entity Framework (Core and v6) – revisited](http://www.thereformedprogrammer.net/architecture-of-business-layer-working-with-entity-framework-core-and-v6-revisited/)

4. [JonPSmith/GenericServices](https://github.com/JonPSmith/GenericServices)
GenericServices helps with building a service/application layer in a .NET based application using EF6.x
## Profile
1. [How-To Profile Entity Framework Core](https://miniprofiler.com/dotnet/HowTo/ProfileEFCore)
2. [cross-app-profiling-demo](https://github.com/teddymacn/cross-app-profiling-demo)

## Mock and Faking
1. [Create test data with NBuilder and Faker](http://www.jerriepelser.com/blog/creating-test-data-with-nbuilder-and-faker/)

2. [BOGUS](https://github.com/bchavez/Bogus)  / [faker.js](https://github.com/marak/Faker.js/)  
可以基于语言生成假数据。
[Sample](https://rawgit.com/Marak/faker.js/master/examples/browser/index.html)
![FakeJs](./Images/FakeJs.png)

## Generic 
1. [Generic Repository Pattern in ASP.NET Core](https://code.msdn.microsoft.com/Generic-Repository-Pattern-f133bca4)

2. [A Truly Generic Repository, Part 1](https://cpratt.co/truly-generic-repository/)
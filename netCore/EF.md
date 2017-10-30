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

代码中，可以看到 EF Core 支持对时间字段 ```c.EventTime``` 取属性 ```Date```，得到只包含日期的字段，用于分组。

## 参考资料
1. [EF Core for Enterprise](https://www.codeproject.com/Articles/1160586/EF-Core-for-Enterprise)

2. [Learn Entity Framework Core](http://www.learnentityframeworkcore.com/)

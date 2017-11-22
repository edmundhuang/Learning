#JSON

1. [Deserialize Abstract Classes with Json.NET](http://www.tomdupont.net/2014/04/deserialize-abstract-classes-with.html)
```cs
public abstract class AbstractJsonConverter<T> : JsonConverter
{
    protected abstract T Create(Type objectType, JObject jObject);
 
    public override bool CanConvert(Type objectType)
    {
        return typeof(T).IsAssignableFrom(objectType);
    }
 
    public override object ReadJson(
        JsonReader reader, 
        Type objectType, 
        object existingValue, 
        JsonSerializer serializer)
    {
        var jObject = JObject.Load(reader);
 
        T target = Create(objectType, jObject);
        serializer.Populate(jObject.CreateReader(), target);
 
        return target;
    }
 
    public override void WriteJson(
        JsonWriter writer, 
        object value, 
        JsonSerializer serializer)
    {
        throw new NotImplementedException();
    }
 
    protected static bool FieldExists(
        JObject jObject, 
        string name, 
        JTokenType type)
    {
        JToken token;
        return jObject.TryGetValue(name, out token) && token.Type == type;
    }
}
 
public class PetConverter : AbstractJsonConverter<Pet>
{
    protected override Pet Create(Type objectType, JObject jObject)
    {
        if (FieldExists(jObject, "FavoriteToy", JTokenType.String))
            return new Dog();
 
        if (FieldExists(jObject, "WantsToKillYou", JTokenType.Boolean))
            return new Cat();
 
        throw new InvalidOperationException();
    }
}
```

unit test
```cs
public abstract class Pet { public string Name { get; set; } }
public class Dog : Pet { public string FavoriteToy { get; set; } }
public class Cat : Pet { public bool WantsToKillYou { get; set; } }

public class AbstractJsonConverterTests
{
    [Fact]
    public void PetConverter()
    {
        var originalArray = new Pet[]
        {
            new Cat { Name = "Sql", WantsToKillYou = true },
            new Cat { Name = "Linq", WantsToKillYou = false },
            new Dog { Name = "Taboo", FavoriteToy = "Sql" }
        };
 
        var json = JsonConvert.SerializeObject(originalArray);
 
        var converter = new PetConverter();
        var deserializedArray = JsonConvert.DeserializeObject<Pet[]>(
            json, 
            converter);
 
        Assert.Equal(originalArray.Length, deserializedArray.Length);
            
        for (var i = 0; i < originalArray.Length; i++)
        {
            var original = originalArray[i];
            var deserialized = deserializedArray[i];
 
            Assert.Equal(original.GetType(), deserialized.GetType());
            Assert.Equal(original.Name, deserialized.Name);
        }
    }
}
```
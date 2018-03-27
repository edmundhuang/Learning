# 异常处理

1. [Error Handling in SOLID C# .NET – The Operation Result Approach](https://www.codeproject.com/Articles/1022462/Error-Handling-in-SOLID-Csharp-NET-The-Operation-R)
``` cs
public class OperationResult<TResult>
{
    private OperationResult ()
    {
    }

    public bool Success { get; private set; }
    public TResult Result { get; private set; }
    public string NonSuccessMessage { get; private set; }
    public Exception Exception { get; private set; }

    public static OperationResult<TResult> CreateSuccessResult(TResult result)
    {
        return new OperationResult<TResult> { Success = true, Result = result};
    }

    public static OperationResult<TResult> CreateFailure(string nonSuccessMessage)
    {
        return new OperationResult<TResult> { Success = false, NonSuccessMessage = nonSuccessMessage};
    }

    public static OperationResult<TResult> CreateFailure(Exception ex)
    {
        return new OperationResult<TResult>
        {
            Success = false,
            NonSuccessMessage = String.Format("{0}{1}{1}{2}", ex.Message, Environment.NewLine, ex.StackTrace),
            Exception = ex
        };
    }
}

public OperationResult<byte[]> TryReadAllBytes(string path)
{
    try
    {
        var bytes = File.ReadAllBytes(path);
        return OperationResult<byte[]>.CreateSuccessResult(bytes);
    }
    catch (FileNotFoundException fileNotFoundException)
    {
        return OperationResult<byte[]>.CreateFailure(fileNotFoundException);
    }
}

void Test()
{
  var result = myStorageService.TryReadAllBytes(path);
  if(result.Success)
  {
      // do something
  }
  else
  {
      Logger.Log(String.Format("Failed to read file from path, {0}: {1}", path, result.NonSuccessMessage));
  }
}
···
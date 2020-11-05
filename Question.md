# C# 語言

### Defferred Execution 
___
1. 解釋一下什麼是 Defferred Execution 
1. 下面標註的3個地方,有哪幾個地方 query 是真正被 execute 的
    ```c#
    IList<Student> studentList = new List<Student>() {
        new Student() { StudentID = 1, StudentName = "Jhon", age = 18 },
        new Student() { StudentID = 2, StudentName = "Steve", age = 21},
        new Student() { StudentID = 3, StudentName = "Bill", age = 18 }
    };

    // 第一
    var teenAgeStudents = from s in studentList where s.age > 12 && s.age < 20 select s;

    // 第二
    foreach(Student teenStudent in teenAgeStudents)
        Console.WriteLine("Student Name: {0}",teenStudent.StudentName);

    studentList.Add(new Student() { StudentID = 6, StudentName = "Martin", age = 16 });

    // 第三
    foreach(Student teenStudent in teenAgerStudents)
        Console.WriteLine("Student Name: {0}",teenStudent.StudentName);
    ```
1. 下面標註的3個地方,有哪幾個地方 query 是真正被 execute 的
    ```c#
    // 第一
    var collection = _context.Post as IQueryable<Post>;

    if (!string.IsNullOrWhiteSpace(postResourceParameter.UserId))
    {
        var userId = postResourceParameter.UserId.Trim();
        // 第二
        collection = collection.Where(p => p.UserId == userId);
    }

    // 第三
    return collection.ToList();
    ```

### GC Memory (記憶體管理的部分)
___
1. 對於下面3個名詞進行解釋
    * Managed Memory
    * Unmanaged Memoery
    * Finalizers

1. 描述一下 IDisposable 的使用時機

1. 解釋一下 public void Dispose() method 裡面兩行代碼的用意
    ```c#

    private bool _disposed = false;

    // 解釋一下 這個 method 裡面兩行代碼的用意
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        if(disposed)
        {
            return;
        }

        if(disposing)
        {
            // Disposing the resources
        }

        _disposed = true;
    }
    ``` 

<br>
<br>
<br>
<br>
<br>



# Dotnet Core Framework

### Dependency Injection in .Net Core
___
1. 有三種 Register Sevice 的 Method,解釋一下這三種方式 Service 的 Scoped Life 有什麼區別
    1. AddSingleton
    1. AddScoped
    1. AddTrasient


<br>
<br>
<br>
<br>
<br>


# DotNet Core Identity

### Claim-Base Model (跟身分認證有關)
___

1. 解釋 Claim, ClaimIdentity, ClaimPrincipal 的關係 or 抽象概念
1. 大概理解一下以下代碼
    ```c#
    // Step 1 
    var driverLicenseClaims = new Claim[]
    {
        new Claim(ClaimTypes.Name, "Po Jen Su"),
        new Claim(ClaimTypes.Email, "brian71742@gmail.com")
    };

    // Step 2
    var driverLicenseIdentity = new ClaimsIdentity(driverLicenseClaims);

    // Step 3
    var userPrincipal = new ClaimsPrincipal( new[] { driverLicenseIdentity } );

    //Step 4
    await HttpContext.SignInAsync(userPrincipal);
    ```
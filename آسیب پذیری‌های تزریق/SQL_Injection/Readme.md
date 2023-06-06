در پیشگیری از بروز حملات SQL Injection سه رویکرد کلی پیشنهاد می­شود:

    استفاده از statement های از پیش آماده‌شده (با parameterized queries)
    استفاده از لیست سفید در اعتبارسنجی ورودی­ها
    statement های از پیش آماده شده

    درواقع روش parameterized query یا prepared statement در مقابل روش استفاده از dynamic query قرار می­گیرد. در این روش برنامه نویس ابتدا تمامی کد SQL را تعریف می­کند، سپس هر پارامتر را به query می­فرستد. این روش پیاده‌سازی به دیتابیس اجازه می­دهد تا فارغ از ورودی کاربر تفاوت بین کد و داده را تشخیص دهد.

توابع پیشنهادی برای بهره­گیری از این روش در زبان مختلف:

    JAVA : استفاده از PreparedStatement() با متغیرهای bind شده
    NET : از SqlCommand() یا OleDbCommand() با متغیرهای bind شده استفاده کنید
    PHP : از PDO با query های parameterize شده استفاده کنید )با bindParam())
    Hibernate : از createQuery() استفاده کنید
    SQLite : از sqlite3_prepare() استفاده کنید

    در مثال زیر از این روش در java استفاده‌شده است

// This should REALLY be validated too
String custname = request.getParameter("customerName"); 
// Perform input validation to detect attacks
String query = "SELECT account_balance FROM user_data WHERE user_name = ? ";
PreparedStatement pstmt = connection.prepareStatement( query );
pstmt.setString( 1, custname); 
ResultSet results = pstmt.executeQuery( );

    در .NET شاید حتی استفاده از این روش ساده‌تر باشد. به مثال زیر در .NET توجه کنید:

String query = "SELECT account_balance FROM user_data WHERE user_name = ?";
try {
  OleDbCommand command = new OleDbCommand(query, connection);
  command.Parameters.Add(new OleDbParameter("customerName", CustomerName Name.Text));
  OleDbDataReader reader = command.ExecuteReader();
  // …
} catch (OleDbException se) {
  // error handling
} 

استفاده از لیست سفید در اعتبارسنجی ورودی­ها
در برخی از بخش­های یک sql query مانند اسم table، اسم ستون یا ترتیب (افزایشی/کاهشی) نمی­توان از متغیرهای bind استفاده نمود. در این مواقع باید از اعتبارسنجی ورودی و طراحی مجدد query کمک گرفت. اگر در قسمتی از برنامه­ی کاربردی اسم یک table بخشی از query است که کاربر با ورودی خود می­سازد، بایستی پارامتر ارسال‌شده توسط کاربر به مقادیر مجاز و در نظر گرفته‌شده برای او map شود تا از قرار گرفتن ورودی کاربر مستقیماً در query جلوگیری شود. توجه کنید که در حالت ایده‌ای این نوع طراحی برنامه­ کاربردی اشتباه بوده و کاربر نباید نیاز به ساختن چنین query هایی داشته باشد.

    یک مثال از این نوع اعتبار سنجی پارامتر ورودی کاربر:

String tableName;
switch(PARAM):
  case "Value1": tableName = "fooTable";
                 break;
  case "Value2": tableName = "barTable";
                 break;
  ...
  default      : throw new InputValidationException("unexpected value provided" 
                                                  + " for table name");

    برای موارد ساده مانند ترتیب داده­ها بهتر است ورودی کاربر به Boolean تبدیل شود و سپس مقدار Boolean در انتخاب پارامتر موردنظر استفاده شود. برای مثال:

public String someMethod(boolean sortOrder) {
 String SQLquery = "some SQL ... order by Salary " + (sortOrder ? "ASC" : "DESC");`
 ...

    در هر شرایطی که ورودی کاربر می­تواند به مقدار غیر string تبدیل شود، مثلاً تاریخ، عدد، Boolean و غیره تبدیل شود، اعمال تبدیل قبل از انتخاب مقادیر موردنظر و ساختن query باعث امن شدن این فرایند می­شود.



### در برنامه زیر ورودی دستور ping از کاربر گرفته می‌شود. و نتیجه به کاربر نشان داده می‌شود.

   ```asp
    <%@ Page Language=&quotC#&quot Debug=&quottrue&quot Trace=&quotfalse&quot %>
    <%@ Import Namespace=&quotSystem.Diagnostics&quot %>
    <%@ Import Namespace=&quotSystem.IO&quot %>
    <script Language=&quotc#&quot runat=&quotserver&quot>
    void Page_Load(object sender, EventArgs e){
    }
    string ExcuteCmd(string arg){
        ProcessStartInfo psi = new ProcessStartInfo();
        psi.FileName = &quotcmd.exe"
        psi.Arguments = &quot/c ping -n 2 &quot + arg;
        psi.RedirectStandardOutput = true;
        psi.UseShellExecute = false;
        Process p = Process.Start(psi);
        StreamReader stmrdr = p.StandardOutput;
        string s = stmrdr.ReadToEnd();
        stmrdr.Close();
        return s;
    }
    void cmdExe_Click(object sender, System.EventArgs e){
        Response.Write(Server.HtmlEncode(ExcuteCmd(addr.Text)));
    }

    <HTML>
    <HEAD>
    <title>ASP.NET Ping Application</title>
    </HEAD>
    <body>
    <form id=&quotcmd&quot method=&quotpost&quot runat=&quotserver&quot>
    <asp:Label id=&quotlblText&quot runat=&quotserver&quot>Command:</asp:Label>
    <asp:TextBox id=&quotaddr&quot runat=&quotserver&quot Width=&quot250px&quot>
    </asp:TextBox>
    <asp:Button id=&quottesting&quot runat=&quotserver&quot Text=&quotexcute&quot =&quotcmdExe_Click&quot>
    </asp:Button>
    </form>
    </body>
    </HTML>
    ```
> در برنامه زیر ورودی دستور ping از کاربر گرفته می‌شود. و نتیجه به کاربر نشان داده نمی‌شود.
```asp
<%@ Page Language=&quotC#&quot Debug=&quottrue&quot Trace=&quotfalse&quot %>
<%@ Import Namespace=&quotSystem.Diagnostics&quot %>
<%@ Import Namespace=&quotSystem.IO&quot %>
<script Language=&quotC#&quot runat=&quotserver&quot>
string ExcuteCmd(string arg){
  ProcessStartInfo psi = new ProcessStartInfo();
  psi.FileName = &quotcmd.exe"
  psi.Arguments = &quot/c ping -n 2 &quot + arg;
  psi.RedirectStandardOutput = true;
  psi.UseShellExecute = false;
  Process p = Process.Start(psi);
  StreamReader stmrdr = p.StandardOutput;
  string s = stmrdr.ReadToEnd();
  stmrdr.Close();
  return s;
}
void Page_Load(object sender, System.EventArgs e){
  string addr = Request.QueryString[&quotaddr&quot];
  Server.HtmlEncode(ExcuteCmd(addr));
}


<HTML>
<HEAD>
<title>ASP.NET Ping Application</title>
</HEAD>
<body>
<form id=&quotcmd&quot method=&quotGET&quot runat=&quotserver&quot>
</form>
</body>
</HTML>
```
> ورودی کاربر حتما باید از نوع ip باشد و به غیر از ip های داخلی مانند 127.0.0.1 باشد.

```asp 
<%@ Page Language=&quotC#&quot Debug=&quottrue&quot Trace=&quotfalse&quot %>
<%@ Import Namespace=&quotSystem.Diagnostics&quot %>
<%@ Import Namespace=&quotSystem.IO&quot %>
<script Language=&quotc#&quot runat=&quotserver&quot>
    void Page_Load(object sender, EventArgs e){
    }
    Boolean Blacklist(string address)
    {
        string[] black_array = { &quot192.168.1.1&quot, &quot127.0.0.1&quot };
        Match match = Regex.Match(address, @&quot^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$&quot);
        if (match.Success)
        {
            if (black_array.Contains(address))
            {
                return false;
            }
            else
            {
                return true;
            }
        }
        return false;

    }
    string ExcuteCmd(string arg){
        if (Blacklist(arg)) {
            ProcessStartInfo psi = new ProcessStartInfo();
            psi.FileName = &quotcmd.exe"
            psi.Arguments = &quot/c ping -n 2 &quot + arg;
            psi.RedirectStandardOutput = true;
            psi.UseShellExecute = false;
            Process p = Process.Start(psi);
            StreamReader stmrdr = p.StandardOutput;
            string s = stmrdr.ReadToEnd();
            stmrdr.Close();
            return s;
        }
        else
        {
            return &quotAccess Denied"
        }

    }
    void cmdExe_Click(object sender, System.EventArgs e){
        Response.Write(Server.HtmlEncode(ExcuteCmd(addr.Text)));
    }


<HTML>
<HEAD>
<title>ASP.NET Ping Application</title>
</HEAD>
<body>
<form id=&quotcmd&quot method=&quotpost&quot runat=&quotserver&quot>
<asp:Label id=&quotlblText&quot runat=&quotserver&quot>Command:</asp:Label>
<asp:TextBox id=&quotaddr&quot runat=&quotserver&quot Width=&quot250px&quot>
</asp:TextBox>
<asp:Button id=&quottesting&quot runat=&quotserver&quot Text=&quotexcute&quot =&quotcmdExe_Click&quot>
</asp:Button>
</form>
</body>
</HTML>
```
> ورودی کاربر نباید شامل برخی از کاراکتر ها مانند  & نباشد.
```asp
<%@ Page Language=&quotC#&quot Debug=&quottrue&quot Trace=&quotfalse&quot %>
<%@ Import Namespace=&quotSystem.Diagnostics&quot %>
<%@ Import Namespace=&quotSystem.IO&quot %>
<script Language=&quotc#&quot runat=&quotserver&quot>
    void Page_Load(object sender, EventArgs e){
    }
    String SafeString(string address)
    {
        char[] separators = new char[]{' ',';',',','\r','\t','\n','&'};

        string[] temp = address.Split(separators, StringSplitOptions.RemoveEmptyEntries);
        address = String.Join(&quot\n&quot, temp);
        return address;
    }
    Boolean Blacklist(string address)
    {
        address = SafeString(address); 
        string[] black_array = { &quot192.168.1.1&quot, &quot127.0.0.1&quot };
        if (black_array.Contains(address))
        {
            return false;
        }
        else
        {

            return true;
        }
    }
    string ExcuteCmd(string arg){
        if (Blacklist(arg)) {
            ProcessStartInfo psi = new ProcessStartInfo();
            psi.FileName = &quotcmd.exe"
            psi.Arguments = &quot/c ping -n 2 &quot + arg;
            psi.RedirectStandardOutput = true;
            psi.UseShellExecute = false;
            Process p = Process.Start(psi);
            StreamReader stmrdr = p.StandardOutput;
            string s = stmrdr.ReadToEnd();
            stmrdr.Close();
            return s;
        }
        else
        {
            return &quotAccess Denied"
        }

    }
    void cmdExe_Click(object sender, System.EventArgs e){
        Response.Write(Server.HtmlEncode(ExcuteCmd(SafeString(addr.Text))));
    }

<HTML>
<HEAD>
<title>ASP.NET Ping Application</title>
</HEAD>
<body>
<form id=&quotcmd&quot method=&quotpost&quot runat=&quotserver&quot>
<asp:Label id=&quotlblText&quot runat=&quotserver&quot>Command:</asp:Label>
<asp:TextBox id=&quotaddr&quot runat=&quotserver&quot Width=&quot250px&quot>
</asp:TextBox>
<asp:Button id=&quottesting&quot runat=&quotserver&quot Text=&quotexcute&quot =&quotcmdExe_Click&quot>
</asp:Button>
</form>
</body>
</HTML>
```

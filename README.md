# DotNet.Framework.GithubActionWorkflow
A simple workflow example of how to build your .Net Framework solution. It can be useful when you try to CI a solution which uses .Net Framework specific project (e.g. Windows Communication Foundation WCF)
## Solution
### Build WCF application without *dotnet build* command
    cd "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\MSBuild\Current\Bin\"
    .\MSBuild.exe $Env:GITHUB_WORKSPACE
This is a workaround for the problem of missing *Microsoft.WebApplication.target*. Build step navigate to *MSBuild* folder which is really ugly and run the *msbuild.exe* on our solution.
*GITHUB_WORKSPACE* is the folder which includes the github project.
### Test only the test project
    cd UnitTestProject1
    dotnet test --no-build
However test project is a .NET Framework project it can be used with *dotnet test* command. The only thing what you should notice here is the navigation to the folder of the test. Otherwise you will get missing *Microsoft.WebApplication.target* error.
## Important to know
 - This solution is full of workarounds (e.g. navigation to the folder of MSBuild)
 - For testing I used *dotnet test* command which cannot be used when you try to test a project which includes WCF parts. So **this solution does not solve the problem of missing Microsoft.WebApplication.target problem** but has a workaround for the problem if your test project is fully separated from the WCF project.
 - It is possible that a perfect solution already exist. In that case please create a new branch with that solution and create a pull request to the master.

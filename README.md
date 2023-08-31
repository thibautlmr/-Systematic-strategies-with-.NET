# Systematic strategies with .NET



## About

The goal of this project is to allow students to work on a financial application, using tools and technologies from the .NET framework. The application to implement is a decision-aid tool for forward and backtests, and during the project, students will get to work with the C# programming language, and they will learn concepts related to database access and gRPC programming with the framework.
To make it easy for you to get started with GitLab, here's a list of recommended next steps.

## Timeline

- Beginning of the project: Aug. 31st
- End of the project: Sept. 7th

## Expected outcome and recommendations

### Expected outcome

There are several possible outcomes, it is expected that every group will be able to produce the outcome from **Milestone 2**. 

**NB:** better grades will not necessarily be obtained by coding functionalities from higher levels, but by ensuring that the code produced at each level is *tested*, *clean* and *easy to read*.

- **Milestone 1.**
A Console Application that can be used to run a test, for given test parameters and market data (the rebalancing oracle parameter can be discarded, and the portfolio rebalanced every day).
- **Milestone 2.**
    A Console Application named ``BacktestConsole``, that can be run from a command prompt using the following command line:
    ```script
    BacktestConsole.exe <test-params> <mkt-data> <output-file>
    ```
    The arguments are the following:
    - ``<test-params>``: path to the JSON file containing the test parameters.
    - ``<mkt-data>``: path to the CSV file containing the market data on which the test will be run.
    - ``<output-file>``: path to the output JSon file containing the values of the replicating portfolio data. The field names should be camelcased.
- **Milestone 3.**
A gRPC couple server/client. 
    - The server should be named ``GrpcBacktestServer``, it is to be invoked for the computation of portfolio replicating data for given test parameters and market data (the *.proto* file is provided). The https endpoint for the server should be https://localhost:7177. 
    - The client should be named ``GrpcEvaluation``, it is to be invoked with the same parameters as ``BacktestConsole`` and should produce the same results. The only difference is that it performs no computations and simply exchanges messages with ``GrpcBacktestServer``.
- **Milestone 3.**
An intelligent implementation of the weekly rebalancing oracle.
- **Milestone 4.**
An intelligent implementation of other financially relevant rebalancing oracles.

### Recommendations
- **Zipped source code of the project.**
The source code must be clean (no *bin*, *obj* or packages directories). It should be possible to compile the source code directly after unzipping it. The name of the zipped folder for group i should be **Group_i.zip**, and the name of the folder should be **Group_i**. For the automated test, the folder must contain the Application Console project named ``BacktestConsole``. The zipped source code should be run through the Python script as soon as possible to make sure the automated tests will be run correctly.

- **Structure of the source code.**
The structure and readability of the code will be two important elements of the final grade, extra care should be taken to make sure the code is clean. 
- **Testing the evaluation script.**
The script that will be used for the evaluation should be tested as soon as possible once **Milestone 2** has been reached. 

## Project resources

### Presentation slides
- On the .NET framework [link](https://www.dropbox.com/scl/fi/jbqae0194200y16qonv9c/PresentationGenerale.pdf?rlkey=gudaiwt6wwngm4dxhmyb544hb&dl=0) 
- On systematic strategies [link](https://www.dropbox.com/scl/fi/txuqryoaztqg50gakldb9/SystematicStrategies.pdf?rlkey=8ejbuj6jiw4a9dusnyc6tygi8&dl=0)

### Pricing library
**Warning:** this Nuget package only works on projects targeting the .NET 7 framework and the Windows operating system.
- Nuget package [link](https://www.dropbox.com/scl/fi/fz5yrpgbwofwdz37hguuz/PricingLibrary.2.0.3.3.nupkg?rlkey=ss97mutfmljlw3xqbjyjgkve3&dl=0)
- Documentation [link](https://www.dropbox.com/scl/fi/nh2zo68pofobzzh4fgosi/PricingLibraryDoc.chm?rlkey=n8ox1naj9qxcrbs3tv4il1gqv&dl=0)

### gRPC protobuf file
- The protobuf file is available [here](Resources/test_params.proto)

### Tests and validation
- Jupyter notebook to analyze the test results [link](Resources/result_analysis.ipynb)
- Several tests cases [folders](Resources/TestData/)

### Evaluation script
- [ReadMe](Resources/EvaluationScript/README.txt)
- [Python script](Resources/EvaluationScript/generate_backtest_results.py)

## Misc

### Microsoft tutorials
- Getting started with Visual Studio 2022: [link](https://www.youtube.com/watch?v=eIHKZfgddLM&t=1s)
- Getting started with gRPC:
	- [link 1](https://docs.microsoft.com/fr-fr/aspnet/core/grpc/)
	- [link 2](https://learn.microsoft.com/fr-fr/aspnet/core/tutorials/grpc/grpc-start)
    
### Installing Visual Studio 2022 Community on a personnal laptop
The following workloads and components should be installed with Visual Studio 2022 for the projects that will take place all year long to work correctly:
- Workloads:
    - ASP.NET
    - .NET Desktop
    - C++ Desktop development
- Individual components:
 - C++/CLI support for the latest build tools

### gRPC configuration. 

During this project, we will be invoking gRPC servers using the https protocol. It is necessary to configure the server deployment, in our case, the localhost port on which the server will be listening. The ports can be configured at the development and the production level: 
        - The configuration for the development level takes place in the **launchSettings.json** file that is available in the Properties folder of the project.
        - The configuration for the production level takes place in the **appsettings.json** file. Below is an example of a configuration for which the server listens to port **7177** of the localhost for the https protocol when launched using the *dotnet* command:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "Kestrel": {
    "EndPoints": {
      "Https": {
        "Url": "https://localhost:7177"
      }
    },
    "EndpointDefaults": {
      "Protocols": "Http2"
    }
}
```



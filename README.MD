<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/WordPress_logo.svg/2000px-WordPress_logo.svg.png" width="400"/>

## WordPress Sample

The goal of this sample is to fully compile an unmodified clone of WordPress into .NET/.NET Core. The project consists of several parts:

- `website` contains sources of WordPress that are compiled into a single .NET Core assembly (`website.dll`) and WordPress content files that will be served by web server.
- `app` project is executable sample ASP.NET Core web server bootstrapping scripts from `website`.
- `dotnet-wp-plugin` is a sample plugin for WordPress written in C#. Its entry-point (`Register` method) is invoked from `peachpieplugin.php` in WordPress plugins directory.

## What does this do?

This sample contains the complete source code of WordPress with none or little  modifications. The purpose is for this code to be compiled by Peachpie, resulting in the output running purely on Microsoft .NET Core. 

Therefore, if everything works as it should, you will see the standard unchanged WordPress in the same way as you would in the traditional PHP version. The difference is that the compiled website runs on .NET Core in the background. 

## How does this work?

The PHP sources in `website` are compiled to .NET Core by Peachpie compiler, which is seamlessly downloaded by *dotnet* itself.

The sample instantiates Kestrel - the opensource web server - and the ASP.NET Core pipeline. The pipeline handles requests to PHP files using the Peachpie `RequestDelegate` by calling the corresponding compiled scripts in `website.dll`.

Note that the original PHP sources (\*.php files) in `website` are not needed to run the compiled application, however, WordPress accesses some files using file-system functions and requires them there.

## Possible Use Cases

- **Improve performance**: compiled code is fast and also optimized by the .NET 'Jitter' for your actual system. Additionally, the .NET performance profiler may be used to resolve bottlenecks.
- **Write plugins in C#**: plugin functionality can be implemented in a separate C# project and/or PHP plugins may use .NET libraries.
- **Integrate WP into a .NET application**: drive the WordPress lifecycle from a C# app, run within the Kestrel Web Server.
- **'Almost' sourceless distribution**: after the compilation, most of the source files are not needed.
- **Take advantage** of the .NET runtime: jittered, secure and manageable platform.
- **Write plugins in C#** in order to provide plugins in .NET with all its advantages like sourceless distribution, type safe and compiled code which is further optimized and checked for actual platform.

## Prerequisites

- .NET Core 1.1 or newer
- MySQL server running on a preconfigured port (3306)
- Optionally - Visual Studio 2017 or Visual Studio Code using the official Peachpie for VSCode extension available on the [Marketplace](https://marketplace.visualstudio.com/items?itemName=iolevel.peachpie-vscode)

## How to run the project

0. start mysql, at `localhost:3306`, user `root`, password `password`
1. `dotnet restore`
2. `cd app`
3. `dotnet run`

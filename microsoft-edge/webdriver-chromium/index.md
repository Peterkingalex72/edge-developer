---
description: Learn how to test your website or app in Microsoft Edge or automate the browser with WebDriver
title: Use WebDriver to automate Microsoft Edge
author: MSEdgeTeam
ms.author: msedgedevrel
ms.date: 08/24/2021
ms.topic: article
ms.prod: microsoft-edge
ms.technology: devtools
keywords: microsoft edge, web development, html, css, javascript, developer, webdriver, selenium, testing, tools, automation, test
---
# Use WebDriver to automate Microsoft Edge

WebDriver allows developers to automate Microsoft Edge by simulating user interaction.  WebDriver tests and simulations differ from JavaScript unit tests in the following ways.

*   Accesses functionality and information not available to JavaScript running in browsers.
*   Simulates user events or OS-level events more accurately.
*   Manages multiple windows, tabs, and webpages in a single test session.
*   Runs multiple sessions of Microsoft Edge on a specific machine.


## Relationship between WebDriver and other software

To automate Microsoft Edge with WebDriver to simulate user interaction, you need three components:

*  Microsoft Edge
*  Microsoft Edge Driver
*  A WebDriver testing framework

The functional relationship between these components is as follows.

| Technology | Role |
|---|---|
| WebDriver | A W3C standard for a platform- and language-neutral wire protocol.  This protocol allows out-of-process programs to remotely instruct the behavior of web browsers. |
| Microsoft Edge Driver | Microsoft's implementation of the WebDriver protocol specifically for Microsoft Edge.  Test authors write tests that use WebDriver commands that Microsoft Edge Driver receives.  Microsoft Edge Driver is then responsible for communicating that command to the browser. |
| A WebDriver testing framework | Test authors use a testing framework to write end-to-end tests and automate browsers.  Provides a language-specific interface that translates your code into commands that Microsoft Edge Driver runs in Microsoft Edge \(Chromium\).  WebDriver testing frameworks exist for all major platforms and languages.  One such framework is Selenium. |
| Internet Explorer Driver | An implementation of the WebDriver protocol specifically for Internet Explorer.  To run legacy end-to-end tests for Internet Explorer, we recommend using Internet Explorer Driver. |

The following sections describe how to get started with WebDriver for Microsoft Edge \(Chromium\).


## Download Microsoft Edge Driver

To begin automating tests, use the following steps to ensure that the WebDriver version you install matches your browser version.

1.  Find your version of Microsoft Edge.
    1.  Navigate to `edge://settings/help`.

        :::image type="complex" source="./media/microsoft-edge-version.msft.png" alt-text="The build number for Microsoft Edge on April 15, 2021" lightbox="./media/microsoft-edge-version.msft.png":::
           The build number for Microsoft Edge on April 15, 2021
        :::image-end:::

1.  Navigate to [Microsoft Edge Driver][MicrosoftDeveloperMicrosoftEdgeToolsWebdriver].
1.  Navigate to **Get the latest version**.
1.  Choose the build of channel that matches your version number of Microsoft Edge.

    :::image type="complex" source="./media/microsoft-edge-driver-install.msft.png" alt-text="The Get the latest version section on the Microsoft Edge Driver webpage" lightbox="./media/microsoft-edge-driver-install.msft.png":::
       The **Get the latest version** section on the [Microsoft Edge Driver][MicrosoftDeveloperMicrosoftEdgeToolsWebdriver] webpage
    :::image-end:::


## Choose a WebDriver testing framework

After downloading Microsoft Edge Driver, the last component you must download is a WebDriver testing framework. Test authors use WebDriver testing frameworks to write end-to-end tests and automate browsers. The framework provides a language-specific interface that translates your code (such as Python, Java, C#, Ruby, or JavaScript) into commands that Microsoft Edge Driver runs in Microsoft Edge \(Chromium\). WebDriver testing frameworks exist for all major platforms and languages.


This article provides instructions for using the Selenium framework, but you can use any library, framework, and programming language that supports WebDriver.  To accomplish the same tasks using a WebDriver testing framework other than Selenium, consult the official documentation for your framework of choice.

If you are using Selenium, the Microsoft Edge team recommends [Selenium 4.0.0-beta2][NugetPackagesSeleniumWebdriver400beta02] or later, because that version of Selenium supports Microsoft Edge \(Chromium\).  However, you can control Microsoft Edge \(Chromium\) in all older versions of Selenium, including the current stable Selenium 3 release.

### Using Selenium 4

The Selenium WebDriver testing framework can be used on any platform, and is available for Java, Python, C#, Ruby, and JavaScript.

Selenium 4 has built-in support for Microsoft Edge (Chromium).  To install Selenium 4, navigate to [Installing Selenium libraries][SeleniumInstallingLibraries].

If you use Selenium 4, you don't need to use Selenium Tools for Microsoft Edge.  Selenium Tools for Microsoft Edge are for Selenium 3 only.  If you try to use Selenium 4 with Selenium Tools for Microsoft Edge and try to create a new `EdgeDriver` instance, you get the following error: `System.MissingMethodException: 'Method not found: 'OpenQA.Selenium.Remote.DesiredCapabilities OpenQA.Selenium.DriverOptions.GenerateDesiredCapabilities(Boolean)'`.

If you're using Selenium 4 and get this error, remove `Microsoft.Edge.SeleniumTools` from your project, and make sure you're using the official `EdgeOptions` and `EdgeDriver` classes from the `OpenQA.Selenium.Edge` namespace.

### Using Selenium 3

If you already use [Selenium 3][SeleniumHQ], you may have existing browser tests and want to add coverage for Microsoft Edge \(Chromium\) without changing your version of Selenium.  To use [Selenium 3][SeleniumHQ] to write automated tests for both Microsoft Edge \(EdgeHTML\) and Microsoft Edge \(Chromium\), install the [Selenium Tools for Microsoft Edge][GithubMicrosoftEdgeSeleniumTools] package to use the updated driver.  The `EdgeDriver` and `EdgeDriverService` classes included in the tools are fully compatible with the built-in equivalents in Selenium 4.

If you are using Selenium 3, use the following steps to add the [Selenium Tools for Microsoft Edge][GithubMicrosoftEdgeSeleniumTools] and [Selenium 3][SeleniumHQ] to your project.

#### [C#](#tab/c-sharp/)

<a id="selenium-tools-install"></a>

Add the [Microsoft.Edge.SeleniumTools][NugetPackagesMicrosoftEdgeSeleniumtools] and [Selenium.WebDriver][NugetPackagesSeleniumWebdriver31410] packages to your .NET project using the [NuGet CLI][NugetCLI] or [Visual Studio][VisualStudio].

#### [Python](#tab/python/)

<a id="selenium-tools-install"></a>

Use [pip][PythonPip] to install the [msedge-selenium-tools][PythonSeleniumTools] and [selenium][PythonSelenium] packages.

```python
pip install msedge-selenium-tools selenium==3.141
```

#### [Java](#tab/java/)

<a id="selenium-tools-install"></a>

If your Java project uses Maven, copy and paste the following dependency to your `pom.xml` file to add [msedge-selenium-tools-java][SonatypeMavenRepositorySearch].

```xml
<dependency>
    <groupId>com.microsoft.edge</groupId>
    <artifactId>msedge-selenium-tools-java</artifactId>
    <version>[3.141.0,)</version>
</dependency>
```

The Java package is also available to download directly on the [Selenium Tools for Microsoft Edge Releases page][GithubMicrosoftEdgeSeleniumToolsReleases].

#### [JavaScript](#tab/javascript/)

<a id="selenium-tools-install"></a>

Use [npm][JavaScriptnpm] to install the [edge-selenium-tools][JavaScriptSeleniumTools] and [selenium-webdriver][JavaScriptSelenium] packages.

```javascript
npm install @microsoft/edge-selenium-tools selenium-webdriver
```

* * *


## Automate Microsoft Edge (Chromium) with WebDriver

To automate a browser using WebDriver, you must first start a WebDriver session using your preferred WebDriver testing framework.  A session is a single running instance of a browser controlled using WebDriver commands.  Start a WebDriver session to launch a new browser instance.  The launched browser instance remains open until you close the WebDriver session.

The following content walks you through using Selenium to start a WebDriver session with Microsoft Edge \(Chromium\).  You can run these examples using either Selenium 3 or 4.  To use WebDriver with Selenium 3, the [Selenium Tools for Microsoft Edge][GithubMicrosoftEdgeSeleniumTools] package must be installed.

> [!NOTE]
> This article provides instructions for using the Selenium framework, but you can use any library, framework, and programming language that supports WebDriver.  To accomplish the same tasks using another framework, consult the official documentation for your framework of choice.

### Automate Microsoft Edge (Chromium)

Selenium uses the `EdgeDriver` class to manage a Microsoft Edge \(Chromium\) session.  To start a session and automate Microsoft Edge \(Chromium\), create a new `EdgeDriver` object and pass it an `EdgeOptions` object with the `UseChromium` property set to `true`.

#### [C#](#tab/c-sharp/)

<a id="drive-microsoft-edge-chromium-code"></a>

```csharp
var options = new EdgeOptions();
options.UseChromium = true;

var driver = new EdgeDriver(options);
```

#### [Python](#tab/python/)

<a id="drive-microsoft-edge-chromium-code"></a>

```python
options = EdgeOptions()
options.use_chromium = True

driver = Edge(options = options)
```

#### [Java](#tab/java/)

<a id="drive-microsoft-edge-chromium-code"></a>

The `EdgeDriver` class only supports Microsoft Edge \(Chromium\), and doesn't support Microsoft Edge \(EdgeHTML\).  For basic usage, you can create an `EdgeDriver` without providing `EdgeOptions`.

```java
EdgeDriver driver = new EdgeDriver();
```

#### [JavaScript](#tab/javascript/)

<a id="drive-microsoft-edge-chromium-code"></a>

```javascript
let options = new edge.Options();
options.setEdgeChromium(true);

let driver = edge.Driver.createSession(options);
```

* * *

> [!NOTE]
> If your IT admin has set the [DeveloperToolsAvailability][DeployedgeMicrosoftEdgePoliciesDevelopertoolsavailability] policy to `2`,  [Microsoft Edge Driver][MicrosoftDeveloperMicrosoftEdgeToolsWebdriver] is blocked from driving Microsoft Edge \(Chromium\), because the driver uses the [Microsoft Edge DevTools][DevtoolsIndex].  Ensure the [DeveloperToolsAvailability][DeployedgeMicrosoftEdgePoliciesDevelopertoolsavailability] policy is set to `0` or `1` to automate Microsoft Edge (Chromium).

### Choose Specific Browser Binaries (Chromium-Only)

You can start a WebDriver session with specific Microsoft Edge \(Chromium\) binaries.  For example, you can run tests using the [Microsoft Edge preview channels][MicrosoftedgeinsiderDownload] such as Microsoft Edge Beta.

#### [C#](#tab/c-sharp/)

<a id="choose-specific-browser-binaries-chrome-only-code"></a>

```csharp
var options = new EdgeOptions();
options.UseChromium = true;
options.BinaryLocation = @"C:\Program Files (x86)\Microsoft\Edge Beta\Application\msedge.exe";

var driver = new EdgeDriver(options);
```

#### [Python](#tab/python/)

<a id="choose-specific-browser-binaries-chrome-only-code"></a>

```python
options = EdgeOptions()
options.use_chromium = True
options.binary_location = r"C:\Program Files (x86)\Microsoft\Edge Beta\Application\msedge.exe"

driver = Edge(options = options)
```

#### [Java](#tab/java/)

<a id="choose-specific-browser-binaries-chrome-only-code"></a>

```java
EdgeOptions options = new EdgeOptions();
options.setBinary("C:\\Program Files (x86)\\Microsoft\\Edge Beta\\Application\\msedge.exe");

EdgeDriver driver = new EdgeDriver(options);
```

#### [JavaScript](#tab/javascript/)

<a id="choose-specific-browser-binaries-chrome-only-code"></a>

```javascript
let options = new edge.Options();
options.setEdgeChromium(true);
options.setBinaryPath("C:\\Program Files (x86)\\Microsoft\\Edge Beta\\Application\\msedge.exe");

let driver = edge.Driver.createSession(options);
```

* * *

### Customize the Microsoft Edge Driver Service

#### [C#](#tab/c-sharp/)

<a id="customize-microsoft-edge-driver-services-code"></a>

When you use the `EdgeOptions` class to create an `EdgeDriver` class instance, it creates and launches the appropriate `EdgeDriverService` class for either Microsoft Edge \(EdgeHTML\) or Microsoft Edge \(Chromium\).

If you want to create an `EdgeDriverService`, use the `CreateChromiumService()` method to create one configured for Microsoft Edge \(Chromium\).  The `CreateChromiumService()` method is useful when you need to add customizations.  For example, the following code starts verbose log output.

```csharp
using (var service = EdgeDriverService.CreateChromiumService())
{
    service.UseVerboseLogging = true;

    var driver = new EdgeDriver(service);
}
```

> [!NOTE]
>You do not need to provide the `EdgeOptions` object when you pass `EdgeDriverService` to the `EdgeDriver` instance.  The `EdgeDriver` class uses the default options for either Microsoft Edge \(EdgeHTML\) or Microsoft Edge \(Chromium\) based on the service you provide.
> However, if you want to provide both `EdgeDriverService` and `EdgeOptions` classes, ensure that both are configured for the same version of Microsoft Edge.  For example, you may use a default Microsoft Edge \(EdgeHTML\) `EdgeDriverService` class and Chromium properties in the `EdgeOptions` class.  The `EdgeDriver` class throws an error to prevent using different versions.

#### [Python](#tab/python/)

<a id="customize-microsoft-edge-driver-services-code"></a>

When you use Python, the `Edge` object creates and manages the `EdgeService`.  To configure the `EdgeService`, pass extra arguments to the `Edge` object as indicated in the following code.

```python
service_args = ['--verbose']
driver = Edge(service_args = service_args)
```

#### [Java](#tab/java/)

<a id="customize-microsoft-edge-driver-services-code"></a>

Use the `createDefaultService()` method to create an `EdgeDriverService` configured for Microsoft Edge \(Chromium\).  Use Java system properties to customize driver services in Java.  For example, the following code uses the `"webdriver.edge.verboseLogging"` property to turn on verbose log output.

```java
System.setProperty("webdriver.edge.verboseLogging", "true");
EdgeDriverService service = EdgeDriverService.createDefaultService();
EdgeOptions options = new EdgeOptions();
EdgeDriver driver = new EdgeDriver(service, options);
```

#### [JavaScript](#tab/javascript/)

<a id="customize-microsoft-edge-driver-services-code"></a>

When you use JavaScript, create and configure a `Service` with the `ServiceBuilder` class.  Optionally, you can pass the `Service` object to the `Driver` object, which starts \(and stops\) the service for you.
To configure the `Service`, run another method in the `ServiceBuilder` class before you use the `build()` method.  Then pass the `service` as a parameter in the `Driver.createSession()` method.

```javascript
let service = new edge.ServiceBuilder().enableVerboseLogging().build();
let driver = edge.Driver.createSession(options, service);
```

* * *

### Use Chromium-Specific Options

If you set the `UseChromium` property to `true`, you can use the `EdgeOptions` class to access the same [Chromium-specific properties and methods][WebdriverCapabilitiesEdgeOptions] that are used when you automate other Chromium browsers.

#### [C#](#tab/c-sharp/)

<a id="use-chromium-specific-options-code"></a>

```csharp
var options = new EdgeOptions();
options.UseChromium = true;
options.AddArgument("headless");
options.AddArgument("disable-gpu");
```

#### [Python](#tab/python/)

<a id="use-chromium-specific-options-code"></a>

```python
options = EdgeOptions()
options.use_chromium = True
options.add_argument("headless")
options.add_argument("disable-gpu")
```

#### [Java](#tab/java/)

<a id="use-chromium-specific-options-code"></a>

```java
EdgeOptions options = new EdgeOptions();
options.addArguments("headless");
options.addArguments("disable-gpu");
```

#### [JavaScript](#tab/javascript/)

<a id="use-chromium-specific-options-code"></a>

```javascript
let options = new edge.Options();
options.setEdgeChromium(true);
options.addArguments("headless");
options.addArguments("disable-gpu");
```

* * *

> [!NOTE]
> If the `UseChromium` property is set to `true`, you are not able to use properties and methods for Microsoft Edge \(EdgeHTML\).


## Other WebDriver installation options

### Docker

If you use [Docker][DockerHub], run the following command to download a pre-configured image with Microsoft Edge \(Chromium\) and [Microsoft Edge Driver][MicrosoftDeveloperMicrosoftEdgeToolsWebdriver] pre-installed.

```console
docker run -d -p 9515:9515 mcr.microsoft.com/msedge/msedgedriver
```

For more information, navigate to the [msedgedriver container on Docker Hub][DockerHubMsedgedriver].


## Testing Internet Explorer

To test sites that require Internet Explorer, use [Internet Explorer Driver][GithubSeleniumHqWikiIEDriver] with Internet Explorer.  Internet Explorer Driver is maintained by the Selenium project.  Even though Microsoft Edge supports IE Mode, you can't use Microsoft Edge Driver with Microsoft Edge to test sites in IE Mode.


## Application Guard

Trusted sites that use Microsoft Defender Application Guard (Application Guard) can be automated using Microsoft Edge Driver.

Untrusted sites that use Application Guard cannot be automated or manipulated using Microsoft Edge Driver.  Application Guard launches untrusted sites in a container, and this container doesn't expose the remote debugging port that Microsoft Edge Driver needs to communicate with the site.

Your enterprise administrator defines what are trusted sites, including cloud resources and internal networks.  Sites that aren't in the trusted sites list are considered untrusted.  Microsoft Edge Driver can automate both InPrivate windows, and sites in the trusted sites list.

For more information about Application Guard, navigate to:

*  [Microsoft Edge support for Microsoft Defender Application Guard][DeployedgeMicrosoftEdgeSecurityWindowsDefenderApplicationGuard]
*  [Microsoft Defender Application Guard overview][WindowsSecurityThreatProtectionMicrosoftDefenderApplicationGuardWindows10]


## Opt out of diagnostic data collection

By default, Microsoft Edge Driver sends diagnostic data such as the status of the [New Session WebDriver command][WebDriverProtocolNewSession] to Microsoft.  To turn off the diagnostic data collection for Microsoft Edge Driver, set the `MSEDGEDRIVER_TELEMETRY_OPTOUT` environment variable to `1`.  For more information about the data that Microsoft Edge Driver collects, navigate to the [Microsoft Edge Privacy Whitepaper][MicrosoftEdgePrivacyWhitepaper].


<!-- ====================================================================== -->
## See also

*  [Selenium documentation][SeleniumDocumentation] - Information about WebDriver in the context of Selenium, and how to write automated WebDriver tests using Selenium.
*  [Contact the Microsoft Edge DevTools team](../devtools-guide-chromium/contact.md) to send feedback about using WebDriver, WebDriver testing frameworks (such as Selenium), and Microsoft Edge.


<!-- ====================================================================== -->
<!-- links -->
[DevtoolsIndex]: ../devtools-guide-chromium/index.md "Microsoft Edge (Chromium) Developer Tools | Microsoft Docs"
[WebdriverCapabilitiesEdgeOptions]: ./capabilities-edge-options.md "Capabilities and EdgeOptions | Microsoft Docs"
[MicrosoftEdgePrivacyWhitepaper]: /microsoft-edge/privacy-whitepaper#microsoft-edge-driver

<!-- external links -->
[DeployedgeMicrosoftEdgePoliciesDevelopertoolsavailability]: /deployedge/microsoft-edge-policies#developertoolsavailability "DeveloperToolsAvailability - Microsoft Edge - Policies | Microsoft Docs"
[DeployedgeMicrosoftEdgeSecurityWindowsDefenderApplicationGuard]: /deployedge/microsoft-edge-security-windows-defender-application-guard "Microsoft Edge support for Microsoft Defender Application Guard | Microsoft Docs"

[WindowsSecurityThreatProtectionMicrosoftDefenderApplicationGuardWindows10]: /windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview "Microsoft Defender Application Guard (Windows 10) - Windows security | Microsoft Docs"

[DockerHub]: https://hub.docker.com "Docker Hub"
[DockerHubMsedgedriver]: https://hub.docker.com/_/microsoft-msedge-msedgedriver?tab=description "msedgedriver | Docker hub"

[GithubMicrosoftEdgeSeleniumTools]: https://github.com/microsoft/edge-selenium-tools "microsoft/edge-selenium-tools | GitHub"
[GithubMicrosoftEdgeSeleniumToolsReleases]: https://github.com/microsoft/edge-selenium-tools/releases "microsoft/edge-selenium-tools | GitHub"
[GithubSeleniumHq]: https://github.com/SeleniumHQ/selenium "SeleniumHQ/selenium | GitHub"
[GithubSeleniumHqWikiIEDriver]: https://github.com/SeleniumHQ/selenium/wiki/InternetExplorerDriver "Internet Explorer Driver - Selenium | GitHub"

[JavaScriptnpm]: https://www.npmjs.com/ "npm"
[JavaScriptSeleniumTools]: https://www.npmjs.com/package/@microsoft/edge-selenium-tools "@microsoft/edge-selenium-tools | npm"
[JavaScriptSelenium]: https://www.npmjs.com/package/selenium-webdriver "selenium-webdriver | npm"

[MicrosoftDeveloperMicrosoftEdgeToolsWebdriver]: https://developer.microsoft.com/microsoft-edge/tools/webdriver "Microsoft Edge Driver | Microsoft Edge Developer"

[MicrosoftEdge]: https://www.microsoft.com/edge "Download New Microsoft Edge Browser"

[MicrosoftedgeinsiderDownload]: https://www.microsoftedgeinsider.com/download "Download Microsoft Edge Insider Channels"

[NugetCLI]:https://www.nuget.org/packages/NuGet.CommandLine/ "NuGet.CommandLine | NuGet Gallery"
[NugetPackagesMicrosoftEdgeSeleniumtools]: https://www.nuget.org/packages/Microsoft.Edge.SeleniumTools "Microsoft.Edge.SeleniumTools | NuGet Gallery"
[NugetPackagesSeleniumWebdriver31410]: https://www.nuget.org/packages/Selenium.WebDriver/3.141.0 "Selenium.WebDriver 3.141.0 | NuGet Gallery"
[NugetPackagesSeleniumWebdriver400beta02]: https://www.nuget.org/packages/Selenium.WebDriver/4.0.0-beta2 "Selenium.WebDriver 4.0.0-beta2 | NuGet Gallery"

[PythonPip]: https://pypi.org/project/pip/ "pip | PyPI"
[PythonSeleniumTools]: https://pypi.org/project/msedge-selenium-tools/ "msedge-selenium-tools | PyPI"
[PythonSelenium]: https://pypi.org/project/selenium/ "selenium | PyPI"

[SeleniumHQ]: https://www.selenium.dev "SeleniumHQ"
[SeleniumDocumentation]: https://www.selenium.dev/documentation "The Selenium Browser Automation Project | Documentation for Selenium"
[SeleniumInstallingLibraries]: https://www.selenium.dev/documentation/en/selenium_installation/installing_selenium_libraries "Installing Selenium libraries | Selenium"

[SonatypeMavenRepositorySearch]: https://search.maven.org/artifact/com.microsoft.edge/msedge-selenium-tools-java/3.141.0/jar "Sonatype Maven Central Repository Search | com.microsoft.edge:msedge-selenium-tools-java"

[TwitterTweetEdgeDevTools]: https://twitter.com/intent/tweet?text=@EdgeDevTools "@EdgeDevTools | Post a tweet"

[VisualStudio]: https://visualstudio.microsoft.com/ "Visual Studio"

[W3CWebdriver]: https://w3.org/TR/webdriver2 "WebDriver | W3C"
[WebDriverProtocolNewSession]: https://www.w3.org/TR/webdriver2/#new-session "8.1 New Session | W3C Working Draft 24 August 2020"

[WikiHeadlessBrowser]: https://en.wikipedia.org/wiki/Headless_browser "Headless browser | Wikipedia"

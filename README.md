# iedup
IntegratorEdu Ping: "Ping" (send telemetry to) your self-hosted IntegratorEdu instance to track hardware

## Compiling
(this program requires Windows, and is only useful for Windows unless fully reprogrammed with similar features)
* clone iedusm (has required file IEdu.cs) from <https://github.com/expertmm/iedusm> into same parent folder as iedup (so iedup and iedusm folders are side by side)
* in windows-target-4.5.1\expertmm run "use.bat" (or compile Release and Debug from <https://github.com/expertmm/Managed-WiFi-API> first preferably)
* Open iedup.sln file in SharpDevelop 5.1 or later (or use .NET 4.0 or later [C# 5.0] command line tools)
* Build, Set configuration, Release
* Build, Build Solution

## Installation
* iedup can only be installed by a priveleged process (due to uiAccess=true in manifest) such as iedusm:
	* build iedup (see compiling above)
	* AND build iedusm (Release configuration) -- see README.md in iedusm
	* right-click iedusm.exe, run as Administrator
### the steps below are DEPRECATED
	* open Administrator command prompt and do the following (but if your Administrator user is not same as user that cloned the projects such as using GitHub Desktop, first edit the file and change the value to DESKTOP_USER to that user):
	  `install_must_be_run_as_Administrator.bat`
	* cd to folder of iedup Release, such as: "cd C:\Users\Owner\
	* `md "%PROGRAMFILES%\iedup"`
	* `cp iedup.exe "%PROGRAMFILES%\iedup\"`
	* cd to folder of iedusm Release
	* run `iedusm`

## Changes
* (2017-12-11) renamed ProjectInstaller (and corresponding cs file) to IEduPInstaller
* (2017-12-04) signed assembly uniquely (different for all projects, since signing key is used to distinguish programs in the GAC)
* (2017-12-01) signed assembly and ManagedWifi.dll (Project Settings, Signing, choose same PublicPrivateKeyFile.snk for all iedu projects) 
* (2017-12-01) 
	* changed iedup solution (project settings, Compiling):
		* Target CPU: 32-bit Intel-compatible processor (was "Any Processor")
	* changed ManagedWifi solution (project settings, Compiling):
		* target .NET 4.0 [C# 5.0]) resolved "found conflicts between different versions of the same dependent assembly"
		* also changed WiFi example Target CPU must be 32-bit otherwise:
			(see also <https://stackoverflow.com/questions/32824080/processor-architecture-mismatch-building-error>)
			* resolved 'There was a mismatch between the processor architecture of the project being build "MSIL" and the processor architecture of the reference "...mscorlib.dll", "x86". . . '
			* (if on "Any Processor") same error for 'reference "System.Data", "AMD64". . .' -- but error goes away and 32-bit is chosen if Target CPU is 32-bit
* (2017-11-29) initial commit

## Known Issues
* won't install ("Access Denied") if adding uiAccess="true" as property of requestedExecutionLevel in manifest, so that service can access GUI elements running at any System integrity level (helps with being able to see UAC prompts) -- see also <https://blogs.msdn.microsoft.com/cjacks/2009/10/15/using-the-uiaccess-attribute-of-requestedexecutionlevel-to-improve-applications-providing-remote-control-of-the-desktop/>
  ("Project," "Project Options," "Applications" tab, change "Embed default manifest" to "Create..." then edit the file that appears).
  * see <http://asprosys.blogspot.com/2009/03/allow-service-to-interact-with-desktop.html>
    found via <https://stackoverflow.com/questions/3351531/how-to-set-interact-with-desktop-in-windows-service-installer>
* regularly get config from server (the following variables):
	* push_interval_ms
	* pull_interval_ms
	* update_interval_hours
	* web_service_base_url

## Authors
### NativeWifi (MIT License)
* https://github.com/consp1racy/NativeWifi by consp1racy
  * based on http://managedwifi.codeplex.com/SourceControl/latest by ikonst (comments on release version say not updated enough for more recent changes to Windows)

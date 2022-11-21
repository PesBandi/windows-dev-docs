If you encounter errors after submitting your app to the Store, you must resolve them in order to continue the [certification process](../../../apps/publish/publish-your-app/app-certification-process.md). The error message will indicate what the problem is and what you might need to do in order to fix the issue. Here is some additional info that can help you resolve these errors.

## UWP apps

If you are submitting a UWP app, you may see an error during preprocessing if your package file is not a .msixupload or .appxupload file generated by Visual Studio for the Store. Be sure that you follow the steps in [Package a UWP app with Visual Studio](/windows/msix/package/packaging-uwp-apps) when creating your app's package file, and only upload the .msixupload or .appxupload file on the [Packages](../../../apps/publish/publish-your-app/upload-app-packages.md) page of the submission, not a .msix/appx or .msixbundle/appxbundle.

If a compilation error is displayed, make sure that you are able to build your application in Release mode successfully. For more info, see [.NET Native Internal Compiler Errors](https://github.com/dotnet/core/blob/master/Documentation/ilcRepro.md).

## Desktop application

If you plan to submit a package that contains both Win32 and UWP binaries, make sure that you create that package by using the Windows Packaging Project that is available in Visual Studio 2017 Update 4 and later versions. If you create the package by using a UWP project template, you might not be able to submit that package to the Store or sideload it onto other PCs. Even if the package publishes successfully, it might behave in unexpected ways on the user's PC. For more info, see [Package an app by using Visual Studio (Desktop Bridge)](/msix/desktop/desktop-to-uwp-packaging-dot-net).

## Windows Phone 8.x and earlier

> [!IMPORTANT]
> As of October 31, 2018, newly-created products cannot include packages targeting Windows Phone 8.x or earlier. For more info, see this [blog post](https://blogs.windows.com/windowsdeveloper/2018/08/20/important-dates-regarding-apps-with-windows-phone-8-x-and-earlier-and-windows-8-8-1-packages-submitted-to-microsoft-store).

You may see **error 2001** when problems with Windows Phone packages are detected during preprocessing. In most cases, you will need to rebuild your app's package to correct the error. Once you've done that, replace the old package with the new one on the [Packages](../../../apps/publish/publish-your-app/upload-app-packages.md) page of the submission before you click **Submit to the Store** again.

There are a number of issues that may cause this error. Review the list below to determine which might apply to your packages.

- **One or more assemblies in the package are obfuscated incorrectly:** Use a different tool to perform the obfuscation, or remove the obfuscation. The compile process optimizes the obfuscated assemblies, but occasionally some assemblies are obfuscated using a tool that modifies the MSIL in an unsupported way that will cause an error.
- **The size of one or more methods in the app exceeds 256 KB of IL:** Refactor the offending method into smaller functions. The size of MSIL for methods in an assembly can be determined by using the ILDASM tool.
- **The strong name signature validation failed for one or more assemblies:** This error typically occurs when the strong name signing was performed using a key different than the one expected in the assembly metadata. Sign with the correct key, or remove strong name signing.
- **The package contains mixed-mode (with managed and native code) assemblies:** Mixed-mode assemblies are not supported on Windows Phone. Remove the mixed-mode assemblies from the package and resubmit the app.
- **A Windows Phone 8.1 XAP or appx/appxbundle assembly is not valid:** Make sure your .winmd file has at least one public entry point. You can use any decompiler application to review the code and check for public entry points if needed.

Another error that you might see after submitting your app is **error 1300**. This occurs when one or more assemblies (or the entire package) is already precompiled. To fix this issue, rebuild the app's package in Microsoft Visual Studio and then submit the newly-generated package.

## Name/identity errors

If you see an error that says **The name found in the package is not one of your reserved app names. Please reserve the app name and/or update your package with the correct app name for this language**, it may be because you’ve entered an incorrect name in your package. This error can also occur if you are using an app name that you haven’t reserved in Partner Center. You can usually resolve this error by following these steps:

- Go to the [App identity](/uwp/publish/view-app-identity-details) page for your app (under **App management**) to confirm whether your app has an assigned Identity. If it doesn’t, you’ll see an option to create one. You’ll need to reserve a name for your app in order to create the Identity. Make sure this is the name you’ve used in your package.
- If your app already has an identity, you might still need to reserve the name that you want to use in your package. Under **App management**, click [Manage app name reservations](../../../apps/publish/partner-center/manage-app-name-reservations.md). Enter the name you’d like to use, and click **Reserve app name**.

> [!IMPORTANT]
> If the name you want to use is not available, another app might have already reserved that name. If your app is already published under that name, or if you think you have the right to use it, [contact support](https://support.microsoft.com/getsupport/hostpage.aspx?locale=EN-US&supportregion=EN-US&ccfcode=US&ln=EN-US&pesid=14654&oaspworkflow=start_1.0.0.0&tenant=store&supporttopic_L1=31762156&supporttopic_L2=31762179).  
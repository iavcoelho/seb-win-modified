This is a repo containing several modifications required to be able to first and most importantly run SafeExamBrowser on a Virtual Machine (I don't like Windows), but also has some other modifications to ensure it works propperly (wink wink).~

## How this is done?

Since SafeExamBrowser is a fully open source application, we can just traverse the ["seb-win-refactoring"](https://github.com/SafeExamBrowser/seb-win-refactoring) repo and search for the files we want to alter.

To alter the files, we will need a .NET debugger and assembly editor. I personally used [dnSpy](https://github.com/dnSpy/dnSpy), because it's free and i like it :). To download it, just select the release tab and click on whatever file makes sense for your computer (Probably will be the x64 though).

## What do we need to change

You can alter anything you want! After all, it's your computer so it will only run the code you want. Anyways, I decided to change the Virtual Machine Detection systems, the Keyboard Hooks and the logging so that I can run it on a VM and the teacher won't know a thing from the log files :)

One outcome of this is that any keyboard shortcut just works, including Alt+Tab (clearly I did not do it on purpose).

## Knowing what to change

Just hop on ["seb-win-refactoring"](https://github.com/SafeExamBrowser/seb-win-refactoring) and search for it! In my case it was the **ScheduleIntegrityVerification** method in SafeExamBrowser.Client.exe file, under [ClientController.cs](https://github.com/SafeExamBrowser/seb-win-refactoring/blob/a3d0ab433b58d3a3d983330d398ce4206bc6eb43/SafeExamBrowser.Client/ClientController.cs#L330) ((I just removed all the logic and made it only log the right sentenced)), the **isVirtualMachine** method in SafeExamBrowser.Monitoring.dll file in the [VirtualMachineDetector](https://github.com/SafeExamBrowser/seb-win-refactoring/blob/a3d0ab433b58d3a3d983330d398ce4206bc6eb43/SafeExamBrowser.SystemComponents/VirtualMachineDetector.cs#L53) class (Just make it return false) and the **KeyboardHookCallback** method in the [KeyboardInterceptor](https://github.com/SafeExamBrowser/seb-win-refactoring/blob/a3d0ab433b58d3a3d983330d398ce4206bc6eb43/SafeExamBrowser.Monitoring/Keyboard/KeyboardInterceptor.cs#L47) class (Just remove the shortcuts you want to be able to use, or remove them all, idc it's your computer not mine. Oh, make sure to return false as well =P).

## In the end

If you learn to use dnSpy this can be quite easy. Just open the .dll file (or .exe), on the sidebar select the class you want to alter, right click on the method and choose _Edit Method C#_. Then change the method to your heart's desire and hit compile. After you've edited all you wanted on the .dll (or .exe), just go on the top bar, hit File and Save Module. Done! You have sucessfully edited your application to run as you wish!

## I dont want to have the trouble

If you dont want to have the trouble (boring), just go on the release tab of this repo, download the dll's and the exe and put them in your SafeExamBrowser\Application folder (Usually in C:\ProgramFiles\SafeExamBrowser\Application\)
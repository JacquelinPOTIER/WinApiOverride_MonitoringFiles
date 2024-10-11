# WinApiOverride Monitoring Files Community Edition

WinApiOverride Monitoring Files are a set of text files used by [WinApiOverride](http://jacquelin.potier.free.fr/winapioverride32/) for monitoring or fuzzing.
They contain API definitions, structures definitions, and define definitions,

## Folders content:
* "monitoring files": WinApiOverride monitoring files that are used for monitoring API calls
* "UserTypes": definition of structures used inside monitoring files
* "UserDefines": defined values used to decode API parameters (allow to display a friendly name instead of raw value)
* "KnownSequences": files containing a list of API calls, used to detect known sequences inside an API set (like FindFirstFileW, FindNextFileW, FindClose)
* "FuzzExclude": API that must not be called when fuzzing dlls (like kernel32|ExitProcess)


## Notes to users
* Content of "monitoring files" folder (without "default" folder) should be duplicated inside "monitoring files/default" to allow to reset monitoring files to there default values inside the "Monitoring File Library" dialog

## Notes to contributors
*Monitoring file syntax description can be found [here](http://jacquelin.potier.free.fr/winapioverride32/doc/monitoringfiles.htm)* \
*User Types file syntax description can be found [here](http://jacquelin.potier.free.fr/winapioverride32/doc/usertypes.htm)* \
*User Defines file syntax description can be found [here](http://jacquelin.potier.free.fr/winapioverride32/doc/userdefines.htm)* \
*WinApiOverride already integrate some well known types internally for better parsing. The list of internally supported types can be found [here](http://jacquelin.potier.free.fr/winapioverride32/doc/monitoringfiles.htm#fullysupported)* 

* Provide only monitoring file for well known dlls (avoid 3rd party dlls) or for well known COM Interfaces
* "UserTypes" and "UserDefines" folders: if content is specific to a module, please put definitions in a subfolder named exactly like the module name
* If some sub-structures are only used by a single structure, you can define the sub-structures in the same file, taking care of defining sub-structures before the main structure
* Use '!' at the begin of a line to disable API which are not common to all windows revision of the same windows version to avoid "Bad code pointer" error message during monitoring file loading for other users. The '!' show the API as unselected inside the "Monitoring File Library" dialog, so API can be activated if required
* Do not specify first bytes analysis results to be portable (first bytes analysis is specific to a single revision)
* Use ":PointedDataSize=ArgX" and ":PointedElementsCount=ArgY" when possible to get more accurate results
* If possible specify API success condition with the failure options (like "|FailureIfNullRet"). In case of failure, this will color the API call background in red inside the main window
* ';' at the begin of a line can be used for comments

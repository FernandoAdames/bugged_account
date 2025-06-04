# bugged_account
IT support scenario involving a corrupted Windows user profile, often encountered in help desk environments.I triggered a profile load failure by renaming the user’s profile folder, which caused Windows to log the user into a temporary profile.  The goal of the project was to diagnose and resolve the issue using tools such as Event Viewer.

🧪 Steps I Took to Solve the Issue

🖥️ Opened Event Viewer

Pressed Win + R, typed eventvwr.msc, and hit Enter to launch Event Viewer.

📂 Navigated to Logs

Went to Windows Logs → Application.

🔍 Filtered the Log

Clicked "Filter Current Log".

Entered Event ID 1511, which is related to user profile load failures.

🧠 Analyzed the Event Message

I'n the general message you'll see a decription along the lines like says the following 
" Windows cannot find the local profile and is logging you on with a temporary profile. Changes you make to this profile will be lost when you log off." 

Found that the user profile couldn’t be loaded because the registry was pointing to a path that didn’t match the current user profile folder.

Found that Windows was unable to load the user profile because the registry key ProfileImagePath was pointing to a user folder that didn’t exist or had been renamed.

🛠️ Fixed the Registry and Folder Mismatch

The ProfileImagePath value under the registry key:

### HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList

was set to a folder name that didn’t match the real profile folder under C:\Users.

Opened regedit and navigated to the appropriate SID under ProfileList.

Located the broken profile and reviewed the ProfileImagePath value.

Opened File Explorer and browsed to C:\Users.

Noticed that the actual user folder name was different from what the registry expected.

Renamed the user folder to exactly match the ProfileImagePath value shown in the registry.



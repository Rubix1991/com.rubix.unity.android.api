# Rubix C# wrappers for Android Java APIs for Unity

This packages provides C# wrappers for Unity for [Android Java APIs](http://developer.android.com/reference).
Under the hood, the package uses [AndroidJavaObject](https://docs.unity3d.com/ScriptReference/AndroidJavaObject.html) and [AndroidJavaProxy](https://docs.unity3d.com/ScriptReference/AndroidJavaProxy.html) for base functionality.

You can find the full list of exposed APIs [here](/Docs~/ExposedApi.md).


## Requirements

* Unity 6000.0.47f1 or higher 
* Unity Android Support
* __Note:__ Older Unity versions are missing required fixes for AndroidJavaObject.

## Samples

TODO

## Examples

The following C# code shows a [toast](https://developer.android.com/guide/topics/ui/notifiers/toasts) and why the wrappers are useful.

```
using Rubix.Unity.Android.Widget;
using Rubix.Unity.Android.App;
...


using var toast = Toast.MakeText(Activity.CurrentActivity, 
    "This is a short toast",
    Toast.LENGTH_SHORT);
toast.Show();
```

Without the wrappers, you would need to manually resolve class names and methods, and the above code would look like this:

```
using UnityEngine.Android;
...

using var unityPlayer = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
using var currentActivity = unityPlayer.GetStatic<AndroidJavaObject>("currentActivity");
using var toastClass = new AndroidJavaClass("android.widget.Toast");
int lengthShort = toastClass.GetStatic<int>("LENGTH_SHORT");
using var toast = toastClass.CallStatic<AndroidJavaObject>("makeText",
    currentActivity,
    "This is a short toast",
    lengthShort);
toast.Call("show");
```
## Android Activity Life Cycle
---
1. **First Start** : onCreate → onStart → onResume.
2. **Minimizing** : onStart → onStop
3. **Maximizing/Resuming** : onRestart → onStart → onResume.
4. **Orientation change** : onStart → onStop → onDestroy → onCreate → onStart → onResume.
5. **Back button** :	onStart → onStop → onDestroy
6. **Start after pressing back button**: Similar to First start.

## Screen Orientation
---
→ We can fix android screen orientation by specifing Screen Orientation in manifest file, but it is not recommended. 

→ We can get callback when screen orientation changes by specifing it in android:configChanges='orientation|screenSize' inside main activity.
and get a call back on onConfigurationChanged(Configuration newConfig).

## Button Click
---
1) using onClick attribute (android:onClick="doSomething")

2) Activity Implements OnClickListener
 → Activity implement OnClickListener
 → Set onclick listner.
 → wait for the Listner.
 
3) Using Inner Class.
→ Create one inner class that implements OnClickListener

4) Interface Variable.(Anonymous Class)

## Activity `onSaveInstanceState()` and `onRestoreInstanceState()`
-------------------------------------------------------------
These method are very usefull in storing important data if activity is destroyed, like in case of screen rotation
As `onSaveInstanceState()` and `onRestoreInstanceState` are called at the time of `onPause()` and `onResume()` respectively.
so, we can store data while `onPause()` and retrive at `onResume()`.

It will not work is user press back button, as android take it as destroying of whole activity.
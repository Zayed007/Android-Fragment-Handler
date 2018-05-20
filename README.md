# Android-Fragment-Handler

```
import android.app.Activity;
import android.app.Fragment;
import android.app.FragmentManager;
import android.app.FragmentTransaction;
import android.content.Context;



import bd.com.cmed.cmedhealthandroiddevices.R;

public class FragmentHandler {
    /**
     * Load fragment by replacing all previous fragments
     * @param fragment
     */
    public static void loadFragment(Fragment fragment, Context context) {
        Activity activity = (Activity) context;
        FragmentManager fragmentManager=activity.getFragmentManager();
        // clear back stack
        for (int i = 0; i < fragmentManager.getBackStackEntryCount(); i++) {
            fragmentManager.popBackStack();
        }
        FragmentTransaction t = fragmentManager.beginTransaction();
        t.replace(R.id.fragmentContainer,fragment);
        fragmentManager.popBackStack();
        // TODO: we have to allow state loss here
        // since this function can get called from an AsyncTask which
        // could be finishing after our app has already committed state
        // and is about to get shutdown.  What we *should* do is
        // not commit anything in an AsyncTask, but that's a bigger
        // change than we want now.
        t.commitAllowingStateLoss();

    }

    /**
     * Load fragment by replacing all previous fragments and assigning tag
     * @param fragment, tag
     */
    public static void loadFragment(Fragment fragment, String tag,Context context) {
        Activity activity = (Activity) context;
        FragmentManager fragmentManager=activity.getFragmentManager();
        // clear back stack
        for (int i = 0; i < fragmentManager.getBackStackEntryCount(); i++) {
            fragmentManager.popBackStack();
        }
        FragmentTransaction t = fragmentManager.beginTransaction();
        t.replace(R.id.fragmentContainer, fragment, tag);
        t.addToBackStack(null);

        // The following pop command was creating problems when loading the
        // required fragment. Just on pushing the fragment to stack, it was
        // being popped and hence, the search on view objects was creating an
        // error.
        // fragmentManager.popBackStack();

        // TODO: we have to allow state loss here
        // since this function can get called from an AsyncTask which
        // could be finishing after our app has already committed state
        // and is about to get shutdown.  What we *should* do is
        // not commit anything in an AsyncTask, but that's a bigger
        // change than we want now.
        t.commitAllowingStateLoss();
    }


    /**
     * Load Fragment on top of other fragments
     * @param fragment
     */
    public static void loadChildFragment(Fragment fragment,Context context) {
        Activity activity = (Activity) context;
        FragmentManager fragmentManager=activity.getFragmentManager();
        FragmentTransaction ft = fragmentManager.beginTransaction();
        ft.replace(R.id.fragmentContainer, fragment, "main")
                .addToBackStack(null)
                .commit();
    }

    /**
     * Load Fragment on top of other fragments by removing last fragment
     * @param fragment, flag
     */
    public static void loadChildFragment(Fragment fragment, boolean flag,Context context) {
        Activity activity = (Activity) context;
        FragmentManager fragmentManager=activity.getFragmentManager();

        if (fragmentManager.getBackStackEntryCount() > 0) {
            fragmentManager.popBackStack();
        }

        FragmentTransaction ft = fragmentManager.beginTransaction();
        ft.replace(R.id.fragmentContainer, fragment, "main")
                .addToBackStack(null)
                .commit();
    }

    public static void popChildFragment(Fragment fragment,Context context) {
        Activity activity = (Activity) context;
        FragmentManager fragmentManager=activity.getFragmentManager();

        if (fragmentManager.getBackStackEntryCount() > 0) {
            fragmentManager.popBackStack();
        }
    }
}
```

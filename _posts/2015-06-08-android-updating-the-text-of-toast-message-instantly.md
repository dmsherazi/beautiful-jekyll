---
ID: 3326
post_title: 'Android: Updating the text of Toast message instantly'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/android-updating-the-text-of-toast-message-instantly/
published: true
post_date: 2015-06-08 08:02:20
---
In my app,I wanted to show the number of taps to be made to accomplish a task, for this purpose i used Toast class , I used Toast.makeText to show the text. problem is that I couldn't change the text or make it hide quickly if new text was to be shown. Android would queue all the makeText requests.

I wanted to have a solution to be able to change the text or be able to cancel the previous toast without waiting for it to finish. While Looking for solution I found this class called Boast by a StackOverFlow user <a href="http://stackoverflow.com/users/383414/richard-le-mesurier">Richard Le Mesurier</a>. The Boast class accomplishes exactly what I needed.

The trick is to keep track of the last <code>Toast</code> that was shown, and to cancel that one.

What Richard Le Mesurier have done is to create a <code>Toast</code> wrapper, that contains a static reference to the last Toast displayed.

When I need to show a new one, I first cancel the static reference, before showing the new one (and saving it in the static).

Here's full code of the <code>Boast</code> wrapper Richard Le Mesurier made - it mimics enough of the Toast methods for me to use it.
<blockquote>By default the <code>Boast</code> will cancel the previous one, so you don't build up a queue of Toasts waiting to be displayed.</blockquote>
This should be a direct drop-in replacement for <code>Toast</code> in most use cases. for example
<pre> mBoast.makeText(this,"your text",Duration).show();</pre>
<pre>import android.annotation.SuppressLint;
import android.content.Context;
import android.content.res.Resources;
import android.widget.Toast;

/**
 * {@link Toast} decorator allowing for easy cancellation of notifications. Use
 * this class if you want subsequent Toast notifications to overwrite current
 * ones. &lt;/p&gt;
 *
 * By default, a current {@link Boast} notification will be cancelled by a
 * subsequent notification. This default behaviour can be changed by calling
 * certain methods like {@link #show(boolean)}.
 */
public class Boast
{
    /**
     * Keeps track of certain {@link Boast} notifications that may need to be cancelled.
     * This functionality is only offered by some of the methods in this class.
     */
    private volatile static Boast globalBoast = null;

    // ////////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * Internal reference to the {@link Toast} object that will be displayed.
     */
    private Toast internalToast;

    // ////////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * Private constructor creates a new {@link Boast} from a given
     * {@link Toast}.
     *
     * @throws NullPointerException
     *         if the parameter is &lt;code&gt;null&lt;/code&gt;.
     */
    private Boast(Toast toast)
    {
        // null check
        if (toast == null)
        {
            throw new NullPointerException(
                    "Boast.Boast(Toast) requires a non-null parameter.");
        }

        internalToast = toast;
    }

    // ////////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * Make a standard {@link Boast} that just contains a text view.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param text
     *        The text to show. Can be formatted text.
     * @param duration
     *        How long to display the message. Either {@link #LENGTH_SHORT} or
     *        {@link #LENGTH_LONG}
     */
    @SuppressLint("ShowToast")
    public static Boast makeText(Context context, CharSequence text,
                                 int duration)
    {
        return new Boast(Toast.makeText(context, text, duration));
    }

    /**
     * Make a standard {@link Boast} that just contains a text view with the
     * text from a resource.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param resId
     *        The resource id of the string resource to use. Can be formatted
     *        text.
     * @param duration
     *        How long to display the message. Either {@link #LENGTH_SHORT} or
     *        {@link #LENGTH_LONG}
     *
     * @throws Resources.NotFoundException
     *         if the resource can't be found.
     */
    @SuppressLint("ShowToast")
    public static Boast makeText(Context context, int resId, int duration)
            throws Resources.NotFoundException
    {
        return new Boast(Toast.makeText(context, resId, duration));
    }

    /**
     * Make a standard {@link Boast} that just contains a text view. Duration
     * defaults to {@link #LENGTH_SHORT}.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param text
     *        The text to show. Can be formatted text.
     */
    @SuppressLint("ShowToast")
    public static Boast makeText(Context context, CharSequence text)
    {
        return new Boast(Toast.makeText(context, text, Toast.LENGTH_SHORT));
    }

    /**
     * Make a standard {@link Boast} that just contains a text view with the
     * text from a resource. Duration defaults to {@link #LENGTH_SHORT}.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param resId
     *        The resource id of the string resource to use. Can be formatted
     *        text.
     *
     * @throws Resources.NotFoundException
     *         if the resource can't be found.
     */
    @SuppressLint("ShowToast")
    public static Boast makeText(Context context, int resId)
            throws Resources.NotFoundException
    {
        return new Boast(Toast.makeText(context, resId, Toast.LENGTH_SHORT));
    }

    // ////////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * Show a standard {@link Boast} that just contains a text view.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param text
     *        The text to show. Can be formatted text.
     * @param duration
     *        How long to display the message. Either {@link #LENGTH_SHORT} or
     *        {@link #LENGTH_LONG}
     */
    public static void showText(Context context, CharSequence text, int duration)
    {
        Boast.makeText(context, text, duration).show();
    }

    /**
     * Show a standard {@link Boast} that just contains a text view with the
     * text from a resource.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param resId
     *        The resource id of the string resource to use. Can be formatted
     *        text.
     * @param duration
     *        How long to display the message. Either {@link #LENGTH_SHORT} or
     *        {@link #LENGTH_LONG}
     *
     * @throws Resources.NotFoundException
     *         if the resource can't be found.
     */
    public static void showText(Context context, int resId, int duration)
            throws Resources.NotFoundException
    {
        Boast.makeText(context, resId, duration).show();
    }

    /**
     * Show a standard {@link Boast} that just contains a text view. Duration
     * defaults to {@link #LENGTH_SHORT}.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param text
     *        The text to show. Can be formatted text.
     */
    public static void showText(Context context, CharSequence text)
    {
        Boast.makeText(context, text, Toast.LENGTH_SHORT).show();
    }

    /**
     * Show a standard {@link Boast} that just contains a text view with the
     * text from a resource. Duration defaults to {@link #LENGTH_SHORT}.
     *
     * @param context
     *        The context to use. Usually your {@link android.app.Application}
     *        or {@link android.app.Activity} object.
     * @param resId
     *        The resource id of the string resource to use. Can be formatted
     *        text.
     *
     * @throws Resources.NotFoundException
     *         if the resource can't be found.
     */
    public static void showText(Context context, int resId)
            throws Resources.NotFoundException
    {
        Boast.makeText(context, resId, Toast.LENGTH_SHORT).show();
    }

    // ////////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * Close the view if it's showing, or don't show it if it isn't showing yet.
     * You do not normally have to call this. Normally view will disappear on
     * its own after the appropriate duration.
     */
    public void cancel()
    {
        internalToast.cancel();
    }

    /**
     * Show the view for the specified duration. By default, this method cancels
     * any current notification to immediately display the new one. For
     * conventional {@link Toast#show()} queueing behaviour, use method
     * {@link #show(boolean)}.
     *
     * @see #show(boolean)
     */
    public void show()
    {
        show(true);
    }

    /**
     * Show the view for the specified duration. This method can be used to
     * cancel the current notification, or to queue up notifications.
     *
     * @param cancelCurrent
     *        &lt;code&gt;true&lt;/code&gt; to cancel any current notification and replace
     *        it with this new one
     *
     * @see #show()
     */
    public void show(boolean cancelCurrent)
    {
        // cancel current
        if (cancelCurrent &amp;&amp; (globalBoast != null))
        {
            globalBoast.cancel();
        }

        // save an instance of this current notification
        globalBoast = this;

        internalToast.show();
    }

}</pre>
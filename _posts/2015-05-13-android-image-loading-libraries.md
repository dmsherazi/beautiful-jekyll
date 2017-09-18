---
ID: 3272
post_title: Android Image Loading Libraries
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/android-image-loading-libraries/
published: true
post_date: 2015-05-13 07:50:54
---
<h2>Asynchronous image loading</h2>
Consider a case where we are having 50 images and 50 titles and we try to load all the images/text into the listview, it won’t display anything until all the images get downloaded.

Here Asynchronous image loading process comes in picture. Asynchronous image loading is nothing but a loading process which happens in background so that it doesn’t block main UI thread and let user to play with other loaded data on the screen. Images will be getting displayed as and when it gets downloaded from background threads.
<h2>Asynchronous image loading libraries</h2>
<ol>
	<li>Nostra’s Universal Image loader – <a title="https://github.com/nostra13/Android-Universal-Image-Loader" href="https://github.com/nostra13/Android-Universal-Image-Loader" target="_blank">https://github.com/nostra13/Android-Universal-Image-Loader</a></li>
	<li>Picasso – <a title="http://square.github.io/picasso/" href="http://square.github.io/picasso/" target="_blank">http://square.github.io/picasso/</a></li>
	<li><a title="https://github.com/koush/UrlImageViewHelper" href="https://github.com/koush/UrlImageViewHelper" target="_blank">UrlImageViewHelper</a> by Koush</li>
	<li><a title="https://android.googlesource.com/platform/frameworks/volley" href="https://android.googlesource.com/platform/frameworks/volley" target="_blank">Volley </a>- By Android team members @ Google</li>
	<li>Novoda’s Image loader – <a title="https://github.com/novoda/ImageLoader" href="https://github.com/novoda/ImageLoader" target="_blank">https://github.com/novoda/ImageLoader</a></li>
</ol>
Let’s have a look at examples using Picasso and Universal Image loader libraries.
<h2>Example 1: Nostra’s Universal Image loader</h2>
<a href="http://www.technotalkative.com/wp-content/uploads/2014/04/UniversalImageLoader.png"><img class="aligncenter size-full wp-image-4791" src="http://www.technotalkative.com/wp-content/uploads/2014/04/UniversalImageLoader.png" alt="Image loading using UniversalImageLoader" width="681" height="446" /></a>

<strong>Step 1: Initialize ImageLoader configuration</strong>
<pre>public class MyApplication extends Application{
@Override
public void onCreate() {
// TODO Auto-generated method stub
super.onCreate();
// Create global configuration and initialize ImageLoader with this configuration
ImageLoaderConfiguration config = new ImageLoaderConfiguration.Builder(getApplicationContext()).build();
ImageLoader.getInstance().init(config);
}
}</pre>
<strong>Step 2: Declare application class inside Application tag in AndroidManifest.xml file</strong>
<pre>&lt;application android:name="MyApplication"&gt;</pre>
<strong>Step 3: Load image and display into ImageView</strong>
<pre>ImageLoader.getInstance().displayImage(objVideo.getThumb(), holder.imgVideo);</pre>
Now, Universal Image loader also provides a functionality to implement success/failure callback to check whether image loading is failed or successful.
<pre>ImageLoader.getInstance().displayImage(photoUrl, imgView,
new ImageLoadingListener() {
@Override
public void onLoadingStarted(String arg0, View arg1) {
// TODO Auto-generated method stub
findViewById(R.id.EL3002).setVisibility(View.VISIBLE);
}
@Override
public void onLoadingFailed(String arg0, View arg1,
FailReason arg2) {
// TODO Auto-generated method stub
findViewById(R.id.EL3002).setVisibility(View.GONE);
}
@Override
public void onLoadingComplete(String arg0, View arg1,
Bitmap arg2) {
// TODO Auto-generated method stub
findViewById(R.id.EL3002).setVisibility(View.GONE);
}
@Override
public void onLoadingCancelled(String arg0, View arg1) {
// TODO Auto-generated method stub
findViewById(R.id.EL3002).setVisibility(View.GONE);
}
});</pre>
<h2>Example 2: Picasso</h2>
<strong>Image loading straight way:</strong>
<pre>Picasso.with(context).load("http://postimg.org/image/wjidfl5pd/").into(imageView);</pre>
<strong>Image re-sizing:</strong>
<pre>Picasso.with(context)
.load(imageUrl)
.resize(100, 100)
.centerCrop()
.into(imageView)</pre>
<h2>Example 3: UrlImageViewHelper library</h2>
<a href="http://www.technotalkative.com/wp-content/uploads/2014/04/helper2.png"><img class="alignleft size-medium wp-image-4804" src="http://www.technotalkative.com/wp-content/uploads/2014/04/helper2-179x300.png" alt="UrlImageViewHelper by Koush" width="179" height="300" /></a>

It’s an android library that sets an ImageView’s contents from a url, manages image downloading, caching, and makes your coffee too.

UrlImageViewHelper will automatically download and manage all the web images and ImageViews. Duplicate urls will not be loaded into memory twice. Bitmap memory is managed by using a weak reference hash table, so as soon as the image is no longer used by you, it will be garbage collected automatically.

<strong>Image loading straight way:</strong>
<pre>UrlImageViewHelper.setUrlDrawable(imgView, "http://yourwebsite.com/image.png");</pre>
<strong>Placeholder image when image is being downloaded:</strong>
<pre>UrlImageViewHelper.setUrlDrawable(imgView, "http://yourwebsite.com/image.png", R.drawable.loadingPlaceHolder);</pre>
<strong>Cache images for a minute only:</strong>
<pre>UrlImageViewHelper.setUrlDrawable(imgView, "http://yourwebsite.com/image.png", null, 60000);</pre>
<h2>Example 4: Volley library</h2>
Yes Volley is a library developed and being managed by some android team members at Google, it was announced by <a title="https://www.youtube.com/watch?v=yhv8l9F44qo" href="https://www.youtube.com/watch?v=yhv8l9F44qo" target="_blank">Ficus Kirkpatrick</a> during the last I/O. I wrote an article about <a title="http://www.technotalkative.com/android-volley-library-example/" href="http://www.technotalkative.com/android-volley-library-example/" target="_blank">Volley library</a> 10 months back <img class="wp-smiley" src="http://www.technotalkative.com/wp-includes/images/smilies/icon_smile.gif" alt=":)" /> , read it and give it a try if you haven’t used it yet.

Let’s look at an example of image loading using Volley.

<strong>Step 1: Take a NetworkImageView inside your xml layout.</strong>
<pre>&lt;com.android.volley.toolbox.NetworkImageView
android:id="@+id/imgDemo"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:scaleType="centerCrop"/&gt;</pre>
<strong>Step 2: Define a ImageCache class</strong>

Yes you are reading title perfectly, we have to define an ImageCache class for initializing ImageLoader object.
<pre>public class BitmapLruCache
extends LruCache&lt;String, Bitmap&gt;
implements ImageLoader.ImageCache {
public BitmapLruCache() {
this(getDefaultLruCacheSize());
}
public BitmapLruCache(int sizeInKiloBytes) {
super(sizeInKiloBytes);
}
@Override
protected int sizeOf(String key, Bitmap value) {
return value.getRowBytes() * value.getHeight() / 1024;
}
@Override
public Bitmap getBitmap(String url) {
return get(url);
}
@Override
public void putBitmap(String url, Bitmap bitmap) {
put(url, bitmap);
}
public static int getDefaultLruCacheSize() {
final int maxMemory =
(int) (Runtime.getRuntime().maxMemory() / 1024);
final int cacheSize = maxMemory / 8;
return cacheSize;
}
}</pre>
<strong>Step 3: Create an ImageLoader object and load image</strong>
Create an ImageLoader object and initialize it with ImageCache object and RequestQueue object.
<pre>ImageLoader.ImageCache imageCache = new BitmapLruCache();
ImageLoader imageLoader = new ImageLoader(Volley.newRequestQueue(context), imageCache);</pre>
<strong>Step 4: Load an image into ImageView</strong>
<pre>NetworkImageView imgAvatar = (NetworkImageView) findViewById(R.id.imgDemo);
imageView.setImageUrl(url, imageLoader);</pre>
<h2>Which library to use?</h2>
Can you decide which library you would use? Let us know which and what are the reasons? <img class="wp-smiley" src="http://www.technotalkative.com/wp-includes/images/smilies/icon_smile.gif" alt=":)" />

Selection of the library is always depends on the requirement. Let’s look at the few fact points about each library so that you would able to compare exactly and can take decision.

<strong>Picasso:</strong>
<ul>
	<li>It’s just a one liner code to load image using Picasso.</li>
	<li>No need to initialize ImageLoader and to prepare a singleton instance of image loader.</li>
	<li>Picasso allows you to specify exact target image size. It’s useful when you have memory pressure or performance issues, you can trade off some image quality for speed.</li>
	<li>Picasso doesn’t provide a way to prepare and store thumbnails of local images.</li>
	<li>Sometimes you need to check image loading process is in which state, loading, finished execution, failed or cancelled image loading. Surprisingly It doesn’t provide a callback functionality to check any state. “fetch()” dose not pass back anything. “get()” is for synchronously read, and “load()” is for asynchronously draw a view.</li>
</ul>
<strong>Universal Image loader (UIL):</strong>
<ul>
	<li>It’s the most popular image loading library out there. Actually, it’s based on the <a title="https://github.com/thest1/LazyList" href="https://github.com/thest1/LazyList" target="_blank">Fedor Vlasov’s project</a></li>
</ul>
which was again probably a very first complete solution and also a <a title="http://stackoverflow.com/questions/541966/how-do-i-do-a-lazy-load-of-images-in-listview/3068012#3068012" href="http://stackoverflow.com/questions/541966/how-do-i-do-a-lazy-load-of-images-in-listview/3068012#3068012" target="_blank">most voted</a> answer (for the image loading solution) on Stackoverflow.
<ul>
	<li>UIL library is better in documentation and even there’s a demo example which highlights almost all the features.</li>
	<li>UIL provides an easy way to download image.</li>
	<li>UIL uses builders for customization. Almost everything can be configured.</li>
	<li>UIL doesn’t not provide a way to specify image size directly you want to load into a view. It uses some rules based on the size of the view. Indirectly you can do it by mentioning ImageSize argument in the source code and bypass the view size checking. It’s not as flexible as Picasso.</li>
</ul>
<strong>Volley:</strong>
<ul>
	<li>It’s officially by Android dev team, Google but still it’s not documented.</li>
	<li>It’s just not an image loading library only but an asynchronous networking library</li>
	<li>Developer has to define ImageCache class their self and has to initialize ImageLoader object with RequestQueue and ImageCache objects.</li>
</ul>
So now I am sure now you can be able to compare libraries. Choosing library is a bit difficult talk because it always depends on the requirement and type of projects. If the project is large then you should go for Picasso or Universal Image loader. If the project is small then you can consider to use Volley librar, because Volley isn’t an image loading library only but it tries to solve a more generic solution.).

I suggest you to start with Picasso. If you want more control and customization, go for UIL.

Read more:
<ol>
	<li><a title="http://blog.bignerdranch.com/3177-solving-the-android-image-loading-problem-volley-vs-picasso/" href="http://blog.bignerdranch.com/3177-solving-the-android-image-loading-problem-volley-vs-picasso/" target="_blank">http://blog.bignerdranch.com/3177-solving-the-android-image-loading-problem-volley-vs-picasso/</a></li>
	<li><a title="http://stackoverflow.com/questions/19995007/local-image-caching-solution-for-android-square-picasso-vs-universal-image-load" href="http://stackoverflow.com/questions/19995007/local-image-caching-solution-for-android-square-picasso-vs-universal-image-load" target="_blank">http://stackoverflow.com/questions/19995007/local-image-caching-solution-for-android-square-picasso-vs-universal-image-load</a></li>
	<li><a title="https://plus.google.com/103583939320326217147/posts/bfAFC5YZ3mq" href="https://plus.google.com/103583939320326217147/posts/bfAFC5YZ3mq" target="_blank">https://plus.google.com/103583939320326217147/posts/bfAFC5YZ3mq</a></li>
</ol>
&nbsp;

VIA <a href="http://www.technotalkative.com" target="_blank">http://www.technotalkative.com</a>
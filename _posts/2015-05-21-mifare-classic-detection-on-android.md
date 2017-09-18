---
ID: 3287
post_title: MiFare Classic Detection on Android
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/mifare-classic-detection-on-android/
published: true
post_date: 2015-05-21 13:09:01
---
Ever since Near Field Communication was embedded on mobile phones, loads of new ideas and business proposals made people very busy. So does the Android platform with its API's supporting NFC. Nexus S looks like a state of the art - good starting point if one wants to get past the monotonic Nokia's piece of the cake. I just want to share with you my experience on reading a MiFare Classic tag using the Nexus S..and the Android platform.
<h4>You need to have:</h4>
<ul>
	<li>A MiFare Classic 1k Tag - ( hopefully you know the keys for its Blocks :=) )</li>
	<li>Android SDK and IDE</li>
	<li>NFC enabled Android  (Make sure if the Android version is 2.3.3 or above).</li>
</ul>
<h3>Some Basics about the card:</h3>
MiFare classic cards store data in its Sectors. In MiFare classic 1k card there are 16 of them. Each Sector contains 4 blocks. You can store 16 bytes in each block. Making about 1024 bytes of storage space..that explains the 1K part of the card. You can perform common tasks like reading, writing data on these blocks, authentification, navigating the card sectors by incrementing the blocks count. The first sector contains manufacturer’s details and a unique id for the card. This is a read only part.

Each sector on the Mifare card is secured by two 48-bit keys: A and B. The last block in the sector contains these keys, as well as a configuration that defines what each key can do with each block, i.e block 0 could be configured so that
key A could read and write, but if a reader authenticates with key B, the reader would only be able to read that block.

The rest of the memory storage can be read or written using keys A and B. Fresh, empty Mifare cards have all their sectors locked with a pair of default keys FFFFFFFFFFFF or 000000000000.
<h6>Default Keys from experiments</h6>
<h3>About the NFC part of Android</h3>
Since ever 2.3.3 Gingerbread - Android exposes an API to read a list of card technologies. To perform operations on a tag, there are three things to be noted.
<ol>
	<li> The cards store data in a format,</li>
	<li> Reading and Writing data is done using a protocol</li>
	<li> Cards support a technology that defines what they are</li>
</ol>
hence reading and writing to these cards can be done only when the data is arranged in that format. MiFare 1K cards support the NDEF format. It also supports NFC - protocol on the communication level. Precisely - ISO 14443 - 3A specification in short NFCA and it uses the MiFare technology.

Now we need to let the Android know what kind of cards we would be using in our application. This is often defined in an XML file stored in the resource folder ( I have named the file - filter_nfc.xml and stored it in a folder named xml). This resource file contains for example,
<pre>android.nfc.tech.NfcA
 android.nfc.tech.MifareClassic</pre>
Here we have declared a tech-list. This list has to be used in the Manifest file. Imagine you would like to start an activity when a tag is touched. The Manifest file is the right place to let the launcher know what activity is to be called when a particular tag is touched.

In the <strong>Manifest file</strong>, you would have an element - activity. This would declare the name of the activity, a title for it and some metadata. Ideally you would let the system know that you want to start this activity when you touch a MiFare classic card. You can define you own filters for different activities for a variety of tag and protocol combinations.

You would then set the permissions on your Manifest file.

You can also do this in your <strong>onCreate</strong> method by using an <strong>NfcAdapter,</strong>
<pre>NfcAdapter mAdapter = NfcAdapter.getDefaultAdapter(this);</pre>
When a MiFare tag is discovered, the NFC stack would get the details of the tag and deliver it to a new Intent of this same activity. Hence to handle this, we would need an instance of the PendingIntent from the current activity.
<pre>PendingIntent mPendingIntent = PendingIntent.getActivity(this, 0,
 new Intent(this, getClass()).addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP), 0);</pre>
Then we could set up our filter which defines the data format and technology type.
<pre>IntentFilter ndef = new IntentFilter(NfcAdapter.ACTION_TECH_DISCOVERED);try {
 ndef.addDataType("*/*");
 } catch (MalformedMimeTypeException e) {
 throw new RuntimeException("fail", e);
 }

 mFilters = new IntentFilter[] {
 ndef,
 };// Setup a tech list for all NfcF tags

 mTechLists = new String[][] { new String[] { MifareClassic.class.getName() } };Intent intent = getIntent();</pre>
Finally when the pending intent calls the activity again, we like to read the tag. I have put all the steps in the method resolveIntent which would do only the reading part of the tag.
<pre>resolveIntent(intent);</pre>
<h3>Reading the tag</h3>
<h6>
The method looks like</h6>
<!--more-->
<pre>private void resolveIntent(Intent intent){
 1) Parse the intent and get the action that triggered this intent
 2) Check if it was triggered by a tag discovered interruption.
 3) Get an instance of the TAG from the NfcAdapter
 4) Get an instance of the Mifare classic card from this TAG instance
 5) Connect to card and get the number of sectors this card has..and loop thru these sectors
 6) In each sector - get the block count, loop thru the blocks, authenticate the sector and read the data
 7) Convert the data into a string from Hex format.
 }</pre>
<h3>filling up with the Android NFC API's</h3>
<pre>void resolveIntent(Intent intent) {
 // 1) Parse the intent and get the action that triggered this intent
 String action = intent.getAction();
 // 2) Check if it was triggered by a tag discovered interruption.
 if (NfcAdapter.ACTION_TECH_DISCOVERED.equals(action)) {
 // 3) Get an instance of the TAG from the NfcAdapter
 Tag tagFromIntent = intent.getParcelableExtra(NfcAdapter.EXTRA_TAG);
 // 4) Get an instance of the Mifare classic card from this TAG intent
 MifareClassic mfc = MifareClassic.get(tagFromIntent);
 byte[] data;
try { // 5.1) Connect to card
 mfc.connect();
 boolean auth = false;
 String cardData = null;
 // 5.2) and get the number of sectors this card has..and loop thru these sectors
 int secCount = mfc.getSectorCount();
 int bCount = 0;
 int bIndex = 0;
 for(int j = 0; j &lt; secCount; j++){
 // 6.1) authenticate the sector
 auth = mfc.authenticateSectorWithKeyA(j, MifareClassic.KEY_DEFAULT);
 if(auth){
 // 6.2) In each sector - get the block count
 bCount = mfc.getBlockCountInSector(j);
 bIndex = 0;
 for(int i = 0; i &lt; bCount; i++){
 bIndex = mfc.sectorToBlock(j);
 // 6.3) Read the block
 data = mfc.readBlock(bIndex);
 // 7) Convert the data into a string from Hex format.
 Log.i(TAG, getHexString(data, data.length));
 bIndex++;
 }
 }else{ // Authentication failed - Handle it
}
 }
 }catch (IOException e) {
 Log.e(TAG, e.getLocalizedMessage());
 showAlert(3);
 }
 }// End of method</pre>
you would have to think about how you like to handle the lifecycle of this activity. I Like to call the reading part of the activity when I detect a tag and if on pause.. would like to disable this. It has been very neatly explained in the Android samples on Foreground dispatch.. I have added this part of the code here too,
<pre>@Override
 public void onResume() {
 super.onResume();
 mAdapter.enableForegroundDispatch(this, mPendingIntent, mFilters, mTechLists);
 }
@Override
 public void onNewIntent(Intent intent) {
 Log.i("Foreground dispatch", "Discovered tag with intent: " + intent);
 resolveIntent(intent);
 }

@Override
 public void onPause() {
 super.onPause();
 mAdapter.disableForegroundDispatch(this);
 }</pre>
Hope this was useful for you. I would try writing to tag on my next blog. If you would find better ideas, please do share.

VIA<a href="http://mifareclassicdetectiononandroid.blogspot.com/"> http://mifareclassicdetectiononandroid.blogspot.com/</a>
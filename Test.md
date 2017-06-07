# Veracity
Analysis of real-time sensor data

## Google Play FAQ

### 1. What is the process for publishing apps and updates?

	To publish any private or public app, you must register as a developer.
    Sign in to the Google Account that will act as the account owner for your developer account.
	Go to the Google Play Console to begin registration.
    Check the agreement box to accept the Google Play Developer distribution agreement. If your account has previously violated this agreement,
		you can't register as a Google Play Developer.
    Click Continue to payment
    Pay the registration fee ($25) and click Accept and continue.
    Enter your Developer account details, including a Developer name which is the name that is displayed in Google Play.
    (It can take up to 48 hours for your Google Play Developer registration to be processed.)
		 
### 2. Do we need a particular type of Google account?
	
	No, any Google account will work with the service.
		 
### 3. How do we setup the device to auto update the app?

	Delivery of updates
    After you’ve submitted an update to an app, you’ll see “Update pending” near the top right of your app’s Play Console pages. Once the update is published,
	your update will start being distributed to existing users.

	Once your update is available, users can download the update on your app’s store listing page or from their My apps page on the Play Store app.
	If a user has turned on automatic updates for your app, the update will be downloaded and installed automatically.
	
### 4. Can we manage when the app is updated remotely?
	
	Once we publish the update, the update will push to the devices. We can use a staged rollout which will deliver to a percentage of devices. However,
	the Console cannot control which devices the update is pushed to.
	
### 5. Does it require package signing?
	
	Android requires that all apps be digitally signed with a certificate before they can be installed.
	For more information, go to the Android Developers site.
	
### 6. Does Google allow you to make your app private or require special permissions?
	
	Publish private apps
	If your organization needs to distribute Android applications to your internal users, you can use managed Google Play to distribute these private apps.
	After you register for a Google Play Developer account and set up the correct administrator privileges to upload and publish the app to managed Google Play,
	you can use the Enterprise Mobility Management (EMM) console to distribute the app to users. For private apps, you have to specify settings so that they're
	only available to users in your enterprise and make them easy to find. You also have to specify certain settings if you're hosting the app, rather than Google.

### 7. What does it mean to sign an APK and how do you do it?

	This is from a tutorial found at: [Understanding Android App Signing](https://coronalabs.com/blog/2014/08/26/tutorial-understanding-android-app-signing/)

#### The Keystore

	The basics behind protecting your Android app is to use a generated certificate and digital “key” which provides a unique, encrypted, and reasonably
	un-hackable signature. This proves that the app came from you, not some other suspicious source. On Android, this is done via a keystore. The keystore
	is a simple file with a really large block of encrypted data. This file can be stored anywhere on your computer, and this is generally the first
	problem that developers encounter. Because there’s no standard location in which to store these, it’s easy to “lose” them — we will address this issue in a bit.
	
	Next, there are two types of keystores that you should be aware of: debug and release. The debug keystore should be used while developing your
	app — for example, it can be used when manually installing (side-loading) apps to local Android devices. However, the debug keystore can not be used
	for an app destined for Google Play or Amazon — for this, you must use a release keystore.
	For both types, a keystore is identified by two aspects: the filename that it’s stored in and an alias. Because a keystore file could potentially
	store multiple keystores, each one is identified by an alias. In most cases, you’ll only have one certificate/key pair in a file, but you still need
	to give it an alias. Keystore files are also protected by a pair of passwords: one for the keystore file itself and another for each keystore/alias
	pair within the file. While these passwords should ideally be unique, most developers use the same password for both.
	
#### Release

	To create a release keystore for your app, you need to execute a command from your OS command line. For OS X, this is done via the Terminal app in
	which you’re presented with a $ prompt. For Windows, this is done via the Command Prompt which can be accessed by opening the Start menu and searching
	for cmd. In Windows, you’ll be presented with a prompt like: C:\> As mentioned above, there’s no standard place to store keystore files, so it may
	be useful to create a folder specifically for this. By default, both the OS X Terminal and Windows Command Prompt will start within your “home” directory.
	On Mac, this translates to /Users/yourloginname and on Windows it translates to something like C:\Users\yourloginname. Within this home folder, you can
	create a folder to hold your keystores.

	* In Windows, type:
		`md Keystores`
	* In OS X, type:
		`mkdir Keystores`

	Once this is done, you can access the folder by typing:
		`cd Keystores`

	Once inside the Keystores directory, you should issue a command that’s fairly complex. Before proceeding, it’s very important to understand that this
	is not a “copy-and-paste” procedure — you must substitute values that are specific to the keystore you wish to generate.
	For the moment, let’s carefully inspect and dissect the following line:

	`keytool -genkey -v -keystore mykeystore.keystore -alias aliasname -keyalg RSA -validity 999999`

	Essentially, the first term means that this line will execute a program called keytool. For OS X, this should be installed already, but Windows users may
	need to install it (see below). Following this, all of the parts that begin with a hyphen (-) indicate parameters for the keytool command. Those options
	are as follows, and those in bold are the two which must be customized (the others can remain as shown):

	* -genkey — Tells keytool to generate a key.
	* -v — Tells keytool to be verbose (i.e. tell you what it’s doing).
	* -keystore — The filename to save the keystore as.
	* -alias — The alias name to identify the keystore.
	* -keyalg RSA — This says to use the RSA method to generate the keystore.
	* -validity 999999 — This says to make the keystore valid for 999,999 days.

	For the keystore name, provide it with a name that makes sense. In theory, you should use a unique release keystore for each app, but it’s not required.
	For example, a puzzle game named “SwapIt” may have a keystore name such as swapit.keystore, but a more general release keystore could simply be release.keystore.
	For alias, provide it with a similar sensible name, for example swapit.
	With these changes, the line should look more like this:

	`keytool -genkey -v -keystore swapit.keystore -alias swapit -keyalg RSA -validity 999999`

	Now hit the return/enter key to execute the command. You’ll then be prompted for more information in a routine that will appear as follows in the command window:

	Enter keystore password:  
	Re-enter new password:
	What is your first and last name?
	  [Unknown]:  YourFirstName YourLastName
	What is the name of your organizational unit?
	  [Unknown]:  Indie      
	What is the name of your organization?
	  [Unknown]:  Your Company Name
	What is the name of your City or Locality?
	  [Unknown]:  YourCity
	What is the name of your State or Province?
	  [Unknown]:  ST
	What is the two-letter country code for this unit?
	  [Unknown]:  US
	Is CN=YourFirstName YourLastName, OU=Indie, O=Your Company Name, L=YourCity, ST=ST, C=US correct?
	  [no]:  yes
	Generating 1,024 bit RSA key pair and self-signed certificate (SHA1withRSA) with a validity of 999,999 days
	for: CN=YourFirstName YourLastName, OU=Indie, O=Your Company Name, L=YourCity, ST=ST, C=US
	Enter key password for
	(RETURN if same as keystore password):  
	Re-enter new password:
	[Storing swapit.keystore]
	
	The first password is the password for the overall keystore file. Next you’ll be asked for your first and last name (surname). The prompt for
	“organizational unit” is for companies with multiple departments like “Engineering” or “Development” and this value is not important for most Corona
	developers, but you need to still provide a value, such as “Development”. In addition, you’ll be prompted for your city, state/province, and country code.
	At this point, you must type in yes to confirm the information. Finally, if desired, you can supply a different password to the individual alias
	entry, or simply press return/enter to use the same password associated with the keystore file.
	
	When this is done, your keystore file will be in the folder where you ran the command.
	
#### Installing “keytool”

	The keytool utility should be installed as part of JDK (Java Development Kit). This tutorial will not discuss actual installation of JDK, so if you’re
	new to this process, please read our corresponding guide.
	On Mac, the keytool utility will be placed in a location such that you can just type keystore in the Terminal to run it. On Windows, this likely
	won’t be the case — when you installed the JDK, it was probably installed within a folder specific to the JDK version. For instance, on my Windows 10 
	computer, it’s located in:
	
	C:\Program Files\Java\jdk1.8.0_131\bin
	
#### Building the App

To build with your release keystore, launch Corona SDK, load your app, and then build for Android (File → Build → Android…). In the Keystore dialog box, click on the Browse… button beside the Keystore pulldown menu. Navigate to where you saved your keystore file and select it from the dialog box, upon which you’ll be prompted to enter the keystore password.
Once it’s loaded, you’ll see that the Key Alias field is empty. Select the proper alias in this pulldown list and click the Build button. Corona will then prompt you to enter the alias password. Once entered correctly, you’ll be taken back to the build screen where you can hit Build again to build the app. Fortunately, for as long as you use this same release keystore/alias, you won’t need to re-enter the passwords each time.
Keyhashes and SHA1 Signatures

When working with third parties like Facebook or Google Play Game Services (GPGS), sometimes you’ll be asked to generate a value from your keystore. For Google Play Game Services, you must use a release keystore for this task. For Facebook, you can develop/test with a debug keystore, but you’ll eventually need to provide them with information for an app signed with a release keystore.
Both a keyhash (used by Facebook) and a SHA1 signature (used by GPGS) are short strings consisting of values that are calculated from the much larger keystore file. While these two are different values, the concept is the same — some standard math is performed on the values in the keystore to generate a unique value that cannot be easily reversed, helping ensure that the keystore hasn’t been altered by a hacker.
Generating a Keyhash

To generate the keyhash, you once again need to use the command line and enter a line which appears complex but in truth consists of just three commands:
keytool -exportcert -alias yourkeyalias -keystore yourkeystore.keystore | openssl sha1 -binary | openssl base64
The three commands taken separately are as follows:
keytool -exportcert -alias yourkeyalias -keystore yourkeystore.keystore
openssl sha1 -binary — uses the SHA1 method of calculating a signature, output as binary.
openssl base64 — outputs the data in Base64.
As you can see, these three commands are separated by pipe (|) characters. The first command runs and outputs its results, which in turn becomes the input for the second command. Then the second command outputs its results which become the input for the third command. This can cause potential issues because, if there’s even a slight problem in an earlier command, the error gets passed on to the next command rather than the expected data.  For instance, if you mis-type your password, this command series will not notify you but rather produce an SHA1 string based on the input of “Invalid Password”.
In any case, as noted earlier in this tutorial, this is not a copy-and-paste command — you must adjust -alias and -keystore to your specific values. When running this command using the keystore created above, the result is:
tZRNBKXmYKOa22HvFl57za4gvU0=
Note the = sign at the end — this indicates the end of the string and it is important.
Generating a SHA1 Signature

GPGS, in contrast, needs a text representation of the SHA1 output. Fortunately, the keytool utility can output this without any additional commands:
keytool -exportcert -alias swapit -keystore swapit.keystore -list -v
After you enter the password, the output will look something like this:
Lua

Alias name: swapit
Creation date: Aug 24, 2014
Entry type: PrivateKeyEntry
Certificate chain length: 1
Certificate[1]:
Owner: CN=YourFirstName YourLastName, OU=Indie, O=Your Company Name, L=YourCity, ST=ST, C=US
Issuer: CN=YourFirstName YourLastName, OU=Indie, O=Your Company Name, L=YourCity, ST=ST, C=US
Serial number: 53fa57f7
Valid from: Sun Aug 24 17:24:07 EDT 2014 until: Sun Jul 20 17:24:07 EDT 4752
Certificate fingerprints:
	 MD5:  66:22:E9:94:EA:14:EA:4A:06:EB:98:8B:DA:2B:25:D2
	 SHA1: B5:94:4D:04:A5:E6:60:A3:9A:DB:61:EF:16:5E:7B:CD:AE:20:BD:4D
	 Signature algorithm name: SHA1withRSA
	 Version: 3
1
2
3
4
5
6
7
8
9
10
11
12
13
14
Alias name: swapit
Creation date: Aug 24, 2014
Entry type: PrivateKeyEntry
Certificate chain length: 1
Certificate[1]:
Owner: CN=YourFirstName YourLastName, OU=Indie, O=Your Company Name, L=YourCity, ST=ST, C=US
Issuer: CN=YourFirstName YourLastName, OU=Indie, O=Your Company Name, L=YourCity, ST=ST, C=US
Serial number: 53fa57f7
Valid from: Sun Aug 24 17:24:07 EDT 2014 until: Sun Jul 20 17:24:07 EDT 4752
Certificate fingerprints:
MD5:  66:22:E9:94:EA:14:EA:4A:06:EB:98:8B:DA:2B:25:D2
SHA1: B5:94:4D:04:A5:E6:60:A3:9A:DB:61:EF:16:5E:7B:CD:AE:20:BD:4D
Signature algorithm name: SHA1withRSA
Version: 3
In this output, the SHA1: line is the string of hex digits which you need to provide to GPGS when setting up your app, as well as the value you need to provide to Google when setting up your app there. Alternatively, if you need the SHA1 signature formatted as a string rather than a colon-separated hex string, use this command:
keytool -exportcert -alias swapit -keystore swapit.keystore | openssl sha1 -hex
	
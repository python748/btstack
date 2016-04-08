# Introduction #
The latest version of BTstack Keyboard allows to hide the soft keyboard from an external Bluetooth keyboard with the CTRL-TAB shortcut. This is done with very little code:

```
void UIKeyboardOrderInAutomatic();
void UIKeyboardOrderOutAutomatic();
BOOL UIKeyboardAutomaticIsOnScreen();

static void toggleKeyboard(UIKeyboardImpl * keyImpl){
	if (UIKeyboardAutomaticIsOnScreen()) {
		UIKeyboardOrderOutAutomatic();
	} else {
		UIKeyboardOrderInAutomatic();
	}
}
```

This motivates the OS to hide/show the keyboard, and applications that follow [Apple's SDK guidelines for receiving Keyboard Notifications](http://developer.apple.com/iPhone/library/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/TextandWeb/TextandWeb.html#//apple_ref/doc/uid/TP40007072-CH20-SW16) adapt their view accordingly. The most obvious mistake is to react on the - (void)textFieldDidBeginEditing:textField delegate method instead of observing UIKeyboardDidShowNotification.

**Important: You cannot just start typing when no keyboard is shown. If it is not shown, e.g. because there is an Edit  button, you first have to activate the on-screen keyboard. Now, you can hide it with CTRL-TAB to use the full screen.**

# Good #
Applications that work correctly after hiding the keyboard, i.e., you can use the full screen for your text. Note: these are unverified user reports
  * Apple Notes
  * Docs To Go
  * eBuddy+
  * IM+
  * MentalNote
  * [Mobile Colloquy](http://colloquy.mobi/)
  * MobileNoter (an app that syncs with Microsoft Onenote)
  * Nimbuzz
  * Notespark
  * [WriteRoom](http://www.hogbaysoftware.com/products/writeroom_iphone)

# OK #
  * Mobile Terminal: it shows its own keyboard. Just double tab the screen and it is gone

# Bad #
Applications that don't work correctly, which means that you cannot use the area below the soft keyboard after it is hidden, because of the reasons detailed above.
  * Apple Mail
  * Apple Messages (keyboard does not hide)
  * Apple Safari (keyboard does not hide)
  * [Documents by SavySoda](http://www.savysoda.com/Documents/)
  * [Evernote](http://www.evernote.com/about/download/iphone/)
  * [FlowChat](http://thebigboss.org/2009/07/06/flowchat-iphone-irc/)
  * Notemaster
  * Office2
  * [QuickOffice](http://www.quickoffice.com/quickoffice_connect_suite_iphone/) - Got no answer to my mail a month ago


---


**If you have more results, please add a comment.**

**If you have an app which you really want to use in full screen, please email their support with a link to this wiki page.**
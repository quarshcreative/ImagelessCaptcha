# ImagelessCaptcha
***
## Advantages

* Keeps your form clean, no ugly captcha images or third-party embedded styles
* Extremely lightweight
* Very easy to implement
* Customizable

## How it works

Creates a random number on every page load, based on your preferences. From that number, it creates the number as a phrase. In the form, you use the phrase to ask the user to enter it as a number. When the form is posted, you simply check to see if the number matches.

## [Try the demo](http://inorganik.net/imagelessCaptcha)

## Setup

Include the imagelessCaptcha class:
`<?php include "imagelessCaptcha.php"; ?>`

Implement the class
`<?php
$imgLess = new imagelessCaptcha();
$intPhrase = $imgLess->formPhrase();
$int = $imgLess->getInt();
?>`

In your form, add a field for number input, and a hidden field with the correct number:
`<label>Imageless Captcha (spam filter):<br>
<?php echo $intPhrase; ?></label>
<input type="number" name="number" step=".1">
<input type="hidden" name="correctNumber" step=".1" value="<?php echo $int; ?>">`

On post submit, check user submitted number against the correct number:
`// on post submit
if (isset($_POST['submit'])) {
	
	...

	// users attempt
	$number = intval($_POST['number']);
	// get correct number from hidden field
	$correctNumber = intval($_POST['correctNumber']);
	
	$errors = array();
	
	// check user-submitted number against correct number
	if ($number != $correctNumber) {
		$errors['captcha'] = "The number you entered for the spam filter is incorrect.";
	}
	if (!$errors) {
		
		// do something here
		
	} 
}`
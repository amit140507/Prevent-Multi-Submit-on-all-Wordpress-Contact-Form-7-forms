# Prevent Multi Submit on all Wordpress Contact Form 7 forms

### Add This Code in **Functions.php** File.



Before            |  After
:-------------------------:|:-------------------------:
![before](https://user-images.githubusercontent.com/100019842/195264508-b15c2006-4d31-4025-b2f7-5f19b44d6352.png)  |  ![after](https://user-images.githubusercontent.com/100019842/195264516-5759591d-8e9f-47f9-9c2e-8fbffbba378b.png)


``` 
// Prevent Multi Submit on all WPCF7 forms
	add_action( 'wp_footer', 'prevent_cf7_multiple_emails' );
	function prevent_cf7_multiple_emails() {
	?>
	<script type="text/javascript">
	var disableSubmit = false;
	jQuery('input.wpcf7-submit[type="submit"]').click(function() {
	    jQuery(':input[type="submit"]').attr('value',"Sending...");
	    if (disableSubmit == true) {
	        return false;
	    }
	    disableSubmit = true;
	    return true;
	})
	  
	var wpcf7Elm = document.querySelector( '.wpcf7' );
	wpcf7Elm.addEventListener( 'wpcf7_before_send_mail', function( event ) {
	    jQuery(':input[type="submit"]').attr('value',"Sent");
	    disableSubmit = false;
	}, false );
	wpcf7Elm.addEventListener( 'wpcf7invalid', function( event ) {
	    jQuery(':input[type="submit"]').attr('value',"Submit")
	    disableSubmit = false;
	}, false );
	</script>
	<?php

	}
``` 

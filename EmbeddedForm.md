1. Add this snippet in your checkout form  

        <form id="checkbook_io" method="POST">
                  <input type="hidden" id="checkbook_var"
                    data-key="PUBLISHABLE KEY"
                    data-amount='10.00' //Amount to be charged
                    data-name="Merchant Name"
                    data-for="Merchant Name"
                    data-description="Your item's description"
                    data-user-email ='buyer_email_address@example.com'
                    data-redirect-url ="http://example.com/callback.php" //This endpoint should host the code written below             
                    data-firstName ='Buyer First Name'
                    data-lastName ="Buyer Last Name"/>
                  <script src="http://checkbook.io/static/api/checkbook.js" class="checkbook-button" id="checkbook_api_js">
                  </script>
        </form>


2. Add this snippet  in the callback URL (PHP)  

        <?php
        $url = "http://www.checkbook.io/api/charge";
        $token = "token returned from checkbook.io";      
        $amount = "10.00"; //Amount to be charged
        $currency = "USD";
        $description = "Your item's description";
    
        $options = array(
          'http'=>array(
            'method'=>"POST",
            'header'=>
              "Accept-language: en\r\n".
              "Content-type: application/x-www-form-urlencoded\r\n",
            'content'=>http_build_query(
                array(            
                    'key'=>'SECRET KEY',
                    'token'=> $token,
                    'amount' => $amount,
                    'currency' => $currency,
                    'description' => $description
                    
                ),'','&'
            )
        ));
    
        $context = stream_context_create($options);
        $refno = file_get_contents($url,false,$context);
        $pos = strpos($refno, "SUCCESS");
        ?>

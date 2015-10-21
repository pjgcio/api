## 1. Add this snippet in your checkout form  

Note: Amount to be charged in cents

Sandbox:

        <form id="checkbook_io" method="POST">
                  <input type="hidden" id="checkbook_var"
                    data-key="PUBLISHABLE KEY"
                    data-amount='100'
                    data-name="Merchant Name"
                    data-for="Merchant Name"
                    data-description="Your item's description"
                    data-user-email ='buyer_email_address@example.com'
                    data-redirect-url ="https://example.com/callback"          
                    data-firstName ='Buyer First Name'
                    data-lastName ='Buyer Last Name'
                    data-env = "sandbox"/>
                  <script src="https://sandbox.checkbook.io/static/api/v1/checkbook.js" class="checkbook-button" id="checkbook_api_js">
                  </script>
        </form>

Production:

        <form id="checkbook_io" method="POST">
                  <input type="hidden" id="checkbook_var"
                    data-key="PUBLISHABLE KEY"
                    data-amount='100'
                    data-name="Merchant Name"
                    data-for="Merchant Name"
                    data-description="Your item's description"
                    data-user-email ='buyer_email_address@example.com'
                    data-redirect-url ="https://example.com/callback"            
                    data-firstName ='Buyer First Name'
                    data-lastName ="Buyer Last Name"/>
                  <script src="https://www.checkbook.io/static/api/v1/checkbook.js" class="checkbook-button" id="checkbook_api_js">
                  </script>
        </form>


## 2. Add this snippet in the callback URL  
For Python (flask):

        @frontend.route('/callback', methods=['POST'])
        def charge():
            token = request.form['token']
            amount = 100 # in cents
            currency = "USD"
            secret_key = 'secret_key'
            website = 'https://www.example.com'
        
            payload = {'key': secret_key,
                       'website': website,
                       'token': token,
                       'amount': amount,
                       'currency': currency,
                       'description': 'Your transaction description'}
        
            r = requests.post("https://www.checkbook.io/api/v1/charge", data=payload)
            #r = requests.post("https://sandbox.checkbook.io/api/v1/charge", data=payload)
            
For Nodejs (express):

        var request = require('request');
        app.use(express.bodyParser());
        
        app.post('/callback', function(request, response){
        	token = request.body.token;
        	amount = 100; //in cents
        	currency = "USD";
        	secret_key = 'secret_key';
        	website = 'https://www.example.com';
        
        	payload = {'key': secret_key,
        		   'website': website,
        		   'token': token,
        		   'amount': amount,
        		   'currency': currency,
        		   'description': 'Your transaction description'}
        
        	request.post(
        	    //'https://sandbox.checkbook.io/api/v1/charge',
        	    'https://www.checkbook.io/api/v1/charge',
        	    { form: payload },
        	    function (error, response, body) {
        		if (!error && response.statusCode == 200) {
        		    console.log(body)
        		}
        	    }
        	);
        });

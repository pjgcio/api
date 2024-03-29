How to use Custom Form feature 
------

 **Step 1: Looking at the files structure**

   Go to [CustomFormTutorial.html][2] and run it locally.


   You will see the Basic theme stand-alone custom Form UI component. There are mainly 3 files involved in building this widget.
   
    - Html FIle      (customFormApi.html)
    - Js File    (customForm_checkbook.js)
    - Serverside handling (handle postback in your backend to make the final charge)  
   

   Explaining Html File      (customFormApi.html)
   
   This file basically includes html code which builds below component’s User Interface. For now this is the basic theme we have gone with, but user can change the UI theme and add classes to override any of our css and build a UI of their own choice. We are giving user full control in changing the layout of the component.
   
   Note: It is important that you must not change any of the ids of the elements because it will be referred in the javascript code. Which will definitely break the flow.
   
   At the bottom of the file we are including Jquery library for us to make the development easier which most other websites may already have. We recommend you use jquery 1.9.1 and dont remove this import. 
   
   `<script src="https://www.checkbook.io/static/js/jquery-1.9.1.min.js"></script>`
   
   
   Following line is checkbook.io’s javascript file which must be included in the page which requires the dependencies of jquery as shown above
   
   <script src="https://www.checkbook.io/static/api/v1/customForm_checkbook.js"></script>


 **Step 2: How to implement this Component**

   Invoking this widget is very simple and literally one line of code.
   
   first create the config object with all the values from the cart and invoke the UI with new Checkbook(config)
   
   Below is the code which sample values passed in the config object.
   
   Note: the config object must be passed during the initialization of the Checkbook object and also all the parameters are mandatory and must have same names as shown below.
   
   
           <script>
           (function(){
               
               var config = {
                   data_key: "testKey",
                   data_amount: "20.45",
                   data_name: "Jr Merchants",
                   data_for: "Jr Merchants",
                   data_description: "2 widgets ($20.00)",
                   data_user_email: "johnsmith4@gmail.com",
                   data_firstName : "john",
                   data_lastName : "smith",
                   data_addr1 : "address Line 1",
                   data_addr2 : "address Line 2",
                   data_city : "san jose",
                   data_state : "California",
                   data_zip : "95050",
                   data_country : "United States"
               };
               
               new Checkbook(config);
               
           })();
           </script>
   
   
   
   After implementing this properly you should be able to see below widget working automatically.


![checkbook check][1]


 **Step 3: Handle postback**

Once custom Form component is up and running as shown in previous step, From that point onwards Checkbook javascript will handle complete behavior of the flow, validation and will perform the real time payment verification.

![checkbook check][3]


Once the real time payment verification is complete, user will see "Send a Check" button screen where user can review and click on "Send a Check" button and make the payment. 

Note:
----

For some reason if you would not want to use "Send a Check" button but use your own cart submit button or any other way is also possible.

`new Checkbook()` object also gives you access to submit() method which basically invokes the payment call for you without using the "Send a Check" button.

Just use the code like below

`var cb = new Checkbook(config);   // as shown in step 1`  
`cb.submit();`


When `cb.submit()` is called then checkbook.js will inject a token in the HTML which you can control where to inject.
Once the token is injected in the form, you can submit the form and get the `token` on your sever side code.


 **Step 4: Final charge call from your backend**

Now, you are responsible to handle the final "/api/v1/charge" call. Make charge call directly to checkbook.io api/charge along with token and other necessary fields as shown in below sample code.
    
API request:

        curl -k https://www.checkbook.io/api/v1/charge \ 
              -d key=your_secret_key \ 
              -d token=2qweq2eq328217weqweeqw32bwq23bdad \
              -d amount=10 \ 
              -d currency=usd \ 
              -d "description=Sample charge for checkbook.io user"




  [1]: http://i.stack.imgur.com/X5C54.png 
  [2]: https://github.com/CheckbookWeb/api/blob/master/samples/CustomFormTutorial.html
  [3]: http://i.imgur.com/hB9F0wu.png

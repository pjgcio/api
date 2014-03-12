 1. Render a form
    (CustomFormTutorial.html) to accept
    bank details on the merchant website
    which also imports checkbook.js. You
    need to populate fields like price,
    email, user address etc in html.
    Also note that there are form fields
    whose names should not be modified.
    
 2. When the form is submitted, checkbook.js will parse out data
    from the form, hit checkbook.io and
    handle all the user interaction. You
    don't have do do anything here. You
    just need to make sure the input and
    div IDs are maintained as specified
    in CustomFormTutorial.html
    
 3. checkbook.io will return a token which will be posted back to an
    endpoint on merchants side
    (configured in data-redirect-url).
    You need to handle this post back,
    make the final "charge" call to
    checkbook.io using the token.
    Example charge call:


        curl http://www.checkbook.io/api/charge \ 
    	-d key=your_secret_key \ 
    	-d token=2qweq2eq328217weqweeqw32bwq23bdad \
    	-d amount=10 \ 
    	-d currency=usd \ 
    	-d "description=Sample charge for checkbook.io user"


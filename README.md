CloudEmotionPHP
===============

##API

###Define

All returns will be json type. Enclude `code` and other info.They may have `info` and  `info_cn`  to show the code's meaning.

Function name with `*` means you must login first. Args with `*` means the parameter is required.

Return Code Define:

		'101'=>'OK.',
		'201'=>'Please login.',
		'202'=>'Already login. Please logout first.',
		'203'=>'Username or password incorrect.',
		'204'=>'SQL Error. We are sorry about that and please contact administrator to solve the issue.',
		'205'=>'Access denied. Your account was baned.',	
		'206'=>'Wrong Password.',
		'207'=>'Please Input Password.',
		'208'=>'Username Illegal.',
		'209'=>'Username existed.',
		'210'=>'Email Address Illegal.',
		'211'=>'Email Address Already Existed.',

###Account Part

Login Function:

    URL:        ./api/account.php?f=login
    Method:     POST
    Args:       u:*		Username        (Char, length < 32. )
                p:*		Password        (Char. Server will do substr(SHA1(Password),0,32). )
                k:      KeepLogin       (1 for on. Server will return an AccessKey if it is on. )
    Return:     code  
				UserId					
                AccessKey               (return when KeepLogin is On. A 64-long Char)
    Others:     Server use Session and AccessKey to keep login. Session livetime depends PHP settings. AccessKey 
                can be use for a month. You can post request with AccessKey so the server will automatic relogin
                and set Session for you.
                
Logout Function:

    URL:        ./api/account.php?f=logout
    Method:     POST (or GET)
    Args:       ak:     AccessKey       
    Return:     code
    Others:     If session is timeout you must carry AccessKey to make the Long-Time-Login logout.

ChangePassworde Function(Login required):

	URL:		./api/account.php?f=changepassword
	Method:		POST
	Args:		op:*	OldPassword		
				np:*	NewPassword		(Char. Don't be empty)
				ak:		AccessKey		
	Return:		code

CheckUsername Function:

	URL:		./api/account.php?f=checkusername
	Method:		POST
	Args:		u:*		Username		
	Return:		code

CheckEmailAddress Function:

	URL:		./api/account.php>f=checkemailaddress
	Method:		POST
	Args:		e:*		EmailAddress	(required, Char, length<128)
	Return:		code

Register Function:

	URL:		./api/account.php?f=register
	Method:		POST
	Args:		u:*		Username		
				p:*		Password		
				e:*		EmailAddress	
	Return:		code
				UserId
				Username
				EmailAddress



# webkiosk-authentication-api
Webkiosk Authentication api to validate credentials of students and teachers of JIIT.

Note: Api is working, but can't be accesed due to ip address being blocked in JIIT so use some proxy or Data Pack.

#Usage:
  This api can be used to validate login requests against webkiosk database.
  
  To validate a request send a get request to 
      
      http://188.166.249.229:9000/login_action
      
      with headers : Content-type: application/json
  
  On correct credentials the response returned is json object:
                  
                  {
                    "error": "",   // If some error occurs error feild of JSON response is not empty
                    "success": "Succcessfully Logged in!"
                  }
  Sample Request using AngularJS:
  
                  var data={ 'user': "13103495",
                		    		'pass': "<Your Password>",
                		    		'usertype': "S",   // "S" for students and "E" for employees
                		    		'date1': "01-12-1994"   // DD-MM-YY or DD MM YY
                		    	};
                		    $http.post("http://188.166.249.229:9000/login_action",data)
                		      .then(function(response)
                		      	{console.log(response);
                		      		 if(response.data.error!="")
                		      		 {
                		      		 	console.log(response.data.error);    
                		      		 }
                		      		else
                		      			{GlobalService.authkey=response.data.authkey;
                		      		 	console.log(response.data);}
                		      	
                		      	}),(function(response){
                		      	$scope.response=response;
                		      	console.log($scope.response.error);
                		      	
                		      });
  
  Other Possible responses include: 
                {
                  "error": "Account Locked. Contact ADMINISTRATOR."
              }
              
              {
                  "error": "Could Not Login,Invalid Details!"
              }
              
              {
               "error": "Could not Connect To Webkiosk Due to Network Error."
              }

  Note: All the responses Whether Successfull or unsuccessful return 200,OK so do not check for error using                response code.
  

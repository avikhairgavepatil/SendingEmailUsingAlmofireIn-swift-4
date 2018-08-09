# SendingEmailUsingAlmofireIn-swift-4


//How to send POST request with “x-www-form-urlencoded” content-type in ios swift4
//post application/x-www-form-urlencoded Alamofire



       

 let headers = [
            "Content-Type": "application/x-www-form-urlencoded"
        ]
        
        let parameters =  [
            "emails":"xyz@gmail.com",
            "reply_to":"rabc@gmail.com"
            "sender_name": "Abc",
            "sender_email": "abc@gmail.com",
            "uname":"Test",
            "upassword":"123",
            "email_body":"Testing 123",
            "subject":"Testing 123"
        ]
        
        Alamofire.request("http://testing/index.php/send/send_emails", method: .post, parameters: parameters, encoding:  URLEncoding.httpBody, headers: headers).responseJSON { (response:DataResponse<Any>) in
            
            switch(response.result) {
            case.success(let data):
                print("success",data)
                self.sendsms()
                
            case.failure(let error):
                print("Not Success",error)
                //self.view.makeToast(message: "Server Error!!")
            }
            
        }
        
        
        # Sending Email Through SMTP using MailCore Library In ios Swift
        steps :
        
      1:-> Install  pod’mailcore2-ios’
      2:-> Import #include <MailCore/MailCore.h> into briding file
      3:-> Code Snapat
         
          
       let smtpSession = MCOSMTPSession()
      
        smtpSession.hostname = "smtp.gmail.com"
        smtpSession.username = "abc@gmail.com" . // user email 
        smtpSession.password = "password" // user email password
        smtpSession.port = 465
        //smtpSession.port = 465
        smtpSession.authType = MCOAuthType.saslPlain
        smtpSession.connectionType = MCOConnectionType.TLS
        smtpSession.connectionLogger = {(connectionID, type, data) in
            if data != nil {
                if let string = NSString(data: data!, encoding: String.Encoding.utf8.rawValue){
                    NSLog("Connectionlogger: \(string)")
                }
            }
        }
        let builder = MCOMessageBuilder()
        builder.header.to = [MCOAddress(displayName: "", mailbox: tempEmail)]
        builder.header.from = MCOAddress(displayName: "sdf", mailbox: "abc@gmail.com")
        builder.header.subject = ""
        builder.htmlBody = ""
        
        let rfc822Data = builder.data()
        let sendOperation = smtpSession.sendOperation(with: rfc822Data)
        sendOperation?.start { (error) -> Void in
            if (error != nil) {
                NSLog("Error sending email: \(error)")
                 SVProgressHUD.dismiss()
                
            } else {
                NSLog("Successfully sent email!")
                
                DispatchQueue.main.async
                    {
 
               
                
            }
        }
        
        
        
    }
       
       
       
       // code Example
        
        

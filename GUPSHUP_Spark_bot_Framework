/** Custom NLP for Cisco Spark**/
function MessageHandler(context, event) {
    context.console.log("test");
    evtMsg = event.message;//Parse Event Message to leverage google translate
    email = event.senderobj.channelid;//Determine Email address of user    
    sparkToken = "Bearer <put your bot token from developer.ciscospark.com here>"; //Define Spark Token
    domain = email.substring(email.lastIndexOf("@") +1, email.lastIndexOf("."));//Parse email domain for security
    partsArray = evtMsg.split(' ');//Split message into array for indexing
    myPartsArray = partsArray.join(" ");//Clean input message of symbols for parsing
    myPartsArrayString = myPartsArray.replace(/[&\/\\#,+()$~%.'":*?<>{}]/g, '');//Strip symbols from sent message for successful analysis
    myPartsArrayStringLower=myPartsArrayString.toLowerCase();
    partsArrayClean = myPartsArrayStringLower.split(' ');//Return the clean Parts Array string (i.e. no symbol) to Parts Array for analysis
    url = "https://api.ciscospark.com/v1/messages";//Spark /Message POST URL
    roomId=event.contextobj.contextid;//Set room ID
    sender = event.senderobj.display;//Obtain the full name of the message sender
    firstName = sender.split(" ",1);//Obtain the first name of the message sender
    regex = /(<([^>]+)>)/ig;//Define Regex
    botTrigger=0;//Control to ensure only one response to NLP is given
    //Define NLP responses
    //Spark Specific
    sparkOverview=[
        " ### Cisco Spark for Developers Overview ",
        "> Make it easy for users to integrate Cisco Spark with apps they love and give developers tools to transform collaboration experiences with APIs and SDKs to integrate, extend and customize those experiences.",
        "* **Native Integrations** - Easily configure automated connections from external applications and services within Spark. Initial native integrations include: Github, PagerDuty, Trello, and Zendesk.",
        "* **App Integration Services** - Connect Spark to hundreds of other applications and services using these integration platforms: Built.io, IFTTT, and Zapier.",
        "* **API's and SDK's** - Use open APIs alone or in tandem to customize Spark capabilities.",
        "* **Check it out...** [Cisco Spark for Developers](https://youtu.be/EEeZ0hIdmbA)"
    ];
    extHelp=[
        " ### I'm at your disposal "+firstName+"! You can talk to me in natural language. Ask me about my favourite topics...",
        "* Want to see an overview of Spark for Dev's? Just ask!",                
        "* I've got some really cool demo's to show you",
        "* I've got the right contacts",
        "* Are you developer? Ask me about some developer resources",
        "* Do you have any event requests?",
        "* I got some great training stuff to get you up to speed!",
        "* For email lookup, you can type `buddy lookup Name-To-Be-Looked-up`",
        "* Ask to see our blog posts!",
        "* how's my driving? Feel free to give me some feedback !<your thoughts and feedback>"
    ];
    intHelp=[
        " ### I'm at your disposal "+firstName+"! You can talk to me in natural language. Ask me about my favourite topics...",
        "* Want to see an overview of Spark for Dev's? Just ask!",               
        "* I've got some really cool demo's to show you",
        "* I've got the right contacts",
        "* Are you developer? Ask me about some developer resources",
        "* I can see that you are Cisco employee, I have some sales goodies",
        "* Do you have any event requests?",
        "* I got some great training stuff to get you up to speed!",
        "* For email lookup, you can type `buddy lookup Name-To-Be-Looked-up`",
        "* Ask to see our blog posts!",
        "* how's my driving? Feel free to give me some feedback!"
    ];
    //Partner demo listings
    partnerDemos=[
        " ### Here are some cool Demo's ",
        "* [AltoCloud](https://youtu.be/4p1Tgc_Df7w)",
        "* [Tagnos](https://youtu.be/XYIXCVzsoBQ)",
        "* [vBrick](https://salesdemo.rev-na.demo.vbrick.com/#/videos/78440f4d-12a8-4537-8e58-4f98398fe555)",
        "* [CloudFuze](https://youtu.be/cAITzn7kHwo)",
        "* [Singlewire](https://singlewire.wistia.com/medias/g4dq2efhe0)",
        "* [Eekona](https://youtu.be/dcZFYAsCMlk)",
        "* [Cloverhound & ServiceNow](https://youtu.be/nFXH2sJV7zM)",
        "* [Cloverhound & Cisco Spark for Education](https://youtu.be/9YeXA4369SY)",
        "* [Qwasi - Platform Overview](https://youtu.be/SKuyVi-JkRA)",
        "* [Qwasi - Use Case Overview](https://youtu.be/rZJ7YM_XSvQ)"
    ];
    contactDetails=[
        " ### Contacts ",
        "* [For product and sales questions](mailto:sparkfordevs@cisco.com)",
        "* [For developer support](mailto:devsupport@ciscospark.com)",
        "* [Or join the Spark room (recommended)](https://developer.ciscospark.com/support.html)",
     ];
    devResource=[
        " ### Cisco Developer Resources ",
        "* [Cisco Spark for Developers](https://developer.ciscospark.com/)",
        "* [Cisco Spark for Developers blog](https://developer.ciscospark.com/blog-home.html)",
        "* [DevNet](http://developer.cisco.com/site/collaboration/)",
        "* [Follow us on Twitter](https://twitter.com/ciscosparkdev)",
        "* [Tropo](https://www.tropo.com/)",
        "* [Tropo Europe](http://www.tropo.eu)"
    ];
    extTraining=[
        " ### Training - Public Facing ",
        "* [Cisco Spark for Developers Learning Labs](https://developer.cisco.com/site/spark/)",
        "* [Cisco Spark and Tropo Webinar Series](http://webinar.tropo.com/)",
        "* [Cisco Spark Ambassador Program](http://ambassador.tropo.com/)"
    ];
    intTraining=[
        " ### Training - Visible to Cisco Internal Only",
        "* [SEVT & PSSVT Jive Group](https://cisco.jiveon.com/groups/vt-collaboration)",
        "* [CTG Talk Series](https://cisco.jiveon.com/docs/DOC-16394)",

    ];
    salesResource=[
        " ### Sales Resource - Visible to Cisco Internal Only",
        "* [Cusomter Presentation (March 2016)](https://docs.cisco.com/share/proxy/alfresco/url?docnum=EDCS-11228665&ver=latest)",
        "* [Cisco Spark Service](https://cisco.jiveon.com/docs/DOC-795130)",
        "* [Cisco Spark SDK - Limited Beta Page](https://cisco.jiveon.com/docs/DOC-1523984)",
        "* [Demo Cisco Spark Bots](http://cs.co/thespot)",
        "* [How-to create a Bot with no programming!](https://cisco.jiveon.com/docs/DOC-795130)",
    ];
    blogUrl=[
        "https://developer.ciscospark.com/blog/blog-details-8285.html",
        "https://developer.ciscospark.com/blog/blog-details-8319.html",
        "https://developer.ciscospark.com/blog/blog-details-8252.html",
        "https://developer.ciscospark.com/blog/blog-details-8251.html",
        "https://developer.ciscospark.com/blog/blog-details-8228.html",
        //"https://developer.ciscospark.com/blog/blog-details-8206.html",
        //"https://developer.ciscospark.com/blog/blog-details-8197.html",
        //"https://developer.ciscospark.com/blog/blog-details-8193.html",
        //"https://developer.ciscospark.com/blog/blog-details-8187.html",
        //"https://developer.ciscospark.com/blog/blog-details-8129.html"
    ];
    //Small Talk
    greetingsResponse=[
        "Hey there "+sender+"!"    
    ];
    presenceResponse=[
        "I sure am! How can I help you today?"
    ];
    ageResponse=[
        "I've seen many moons, "+firstName+", I'd rather not say!"
    ];
    wellResponse=[
        "I'm awesome! How are you?"
    ];
    thanksResponse=[
        "You're welcome"
    ];
    //Corresponding NLP definitions
    greetings=[
        "hello",
        "hi",
        "hey",
        "hola",
        "greetings",
        "on",
        "begin",
        "start"
    ];
    thanks=[
        "thanks",
        "thank",
        "gracias",
    ];
    overview=[
        "spark",
        "introduction",
        "overview",
        "description",
        "intro",
        "API"
    ];
    demos=[
        "demo",
        "demos",
        "examples",
        "demonstration",
        "samlples",
        "video",
        "demonstrations",
        "demo's",
        "demonstration's"
    ];
    training=[
        "training",
        "trainings",
        "education",
        "docs",
        "lab",
        "learn"
    ];
    events=[
        "event",
        "events",
        "tradeshow",
        "hackathon",
        "workshop"
    ];
    devResources=[
        "developer",
        "developers",
        "support",
        "dev",
        "coding",
    ];
    salesResources=[
        "sales",
        "sale",
        "presentations",
        "presentation",
        "goodies"
    ];
    contacts=[
        "contact",
        "contacts",
        "address",
        "email"
    ];
    feedback=[
        "feedback",
        "suggest",
        "bug",
        "issue",
        "defect",
    ];
    help=[
        "help",
        "howto",
        "menu",
        "options",
        "begin",
        "start"
    ];
    blog=[
        "blogs",
        "blog"
    ];
    //NLP for a lonely bot mention
    if(partsArrayClean.length<="1"){
            if(domain=="cisco"){
                getinthelp(context,event);
            }else{getexthelp(context,event)}
    }
    //NLP for Blog   
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<blog.length-1;x++){
                if (partsArrayClean[i]===blog[x]){
                    getBlog(context,event);
                }
            }
        }
    }
    //NLP for Lookup
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            if (partsArrayClean[i]==="lookup"){
                lookUpArray = partsArrayClean.slice(1);//Index everything after the second word to determine the input query string 
                lookUpQueryRaw = lookUpArray.join(" ");//Convert from Array to string, seperated by spaces
                lookUpQuery = encodeURI(lookUpQueryRaw);
                var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
                var body = JSON.stringify({"roomId":""+roomId,"markdown":"_Responses limited to 20. Profile pics shown where available_"});
                context.simplehttp.makePost(url,body,header);
                getLookUp(context,event);
            }
        }
    }
    //NLP for Overview
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<overview.length;x++){
                if (partsArrayClean[i]===overview[x]){
                    getoverview(context,event);
                }
            }
        }
    }
    //NLP for Demos
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<demos.length;x++){
                if (partsArrayClean[i]===demos[x]){
                    getdemos(context,event);
                }
            }
        }
    }
    //NLP for Training
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<training.length;x++){
                if (partsArrayClean[i]===training[x]){
                    getExtTraining(context,event);
                }
            }
        }
    }
    //NLP for Events
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<events.length;x++){
                if (partsArrayClean[i]===events[x]){
                    getevents(context,event);
                }
            }
        }
    }
    //NLP for devResources
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<devResources.length;x++){
                if (partsArrayClean[i]===devResources[x]){
                    getDevResources(context,event);
                }
            }
        }
    }
    //NLP for salesResources
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<salesResources.length;x++){
                if (partsArrayClean[i]===salesResources[x]){
                    getsalesResources(context,event);
                }
            }
        }
    }
    //NLP for contacts
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<contacts.length;x++){
                if (partsArrayClean[i]===contacts[x]){
                    getcontacts(context,event);
                }
            }
        }
    }
    //NLP for Feedback
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<feedback.length;x++){
                if (partsArrayClean[i]===feedback[x]){
                    getfeedback(context,event);
                }
            }
        }
    }
    //NLP for Help
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<help.length;x++){
                if (partsArrayClean[i]===help[x]){
                    if(domain=="cisco"){
                        getinthelp(context,event);
                    }else{getexthelp(context,event)}
                }
            }
        }
    }
    //NLP for greeting
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<greetings.length;x++){
                if (partsArrayClean[i]===greetings[x]){
                    getGreeting(context,event);
                }
            }
        }
    }
    //NLP for Thanks
    for (i = 0; i < partsArrayClean.length; i++) {
        if(botTrigger=="0"){
            for (x=0;x<thanks.length;x++){
                if (partsArrayClean[i]===thanks[x]){
                    getThanks(context,event);
                }
            }
        }  
    }    
    //NLP for bot presence
    if(botTrigger=="0"){
        for (i = 0; i < partsArrayClean.length; i++) {
            if (partsArrayClean[i]==="are"){
                for (i = 0; i < partsArrayClean.length; i++) {
                    if (partsArrayClean[i]==="you"){
                        for (i = 0; i < partsArrayClean.length; i++) {
                            if (partsArrayClean[i]==="there"){
                                getPresenceResponse(context,event);
                            }
                        }
                    }
                }
            }
        }
    }
    //NLP for age interaction
    if(botTrigger=="0"){
        for (i = 0; i < partsArrayClean.length; i++) {
            if (partsArrayClean[i]==="how"){
                for (i = 0; i < partsArrayClean.length; i++) {
                    if (partsArrayClean[i]==="old"){
                        for (i = 0; i < partsArrayClean.length; i++) {
                            if (partsArrayClean[i]==="you"){
                                getAgeResponse(context,event);
                            }
                        }
                    }
                }
            }
        
        }
    }
    //NLP for well interaction
    if(botTrigger=="0"){
        for (i = 0; i < partsArrayClean.length; i++) {
            if (partsArrayClean[i]==="how"){
                for (i = 0; i < partsArrayClean.length; i++) {
                    if (partsArrayClean[i]==="are"){
                        for (i = 0; i < partsArrayClean.length; i++) {
                            if (partsArrayClean[i]==="you"){
                                getWellResponse(context,event);
                            }
                        }
                    }
                }
            }
        }
    }
}//END
        /** Functions declared below are required **/
        function EventHandler(context, event) {
            if(! context.simpledb.botleveldata.numinstance)
                context.simpledb.botleveldata.numinstance = 0;
            numinstances = parseInt(context.simpledb.botleveldata.numinstance) + 1;
            context.simpledb.botleveldata.numinstance = numinstances;
            context.sendResponse("Hey, thanks for adding me! To see what I'm all about, just do an @mention help, i.e. @buddy help");
        }
        function getLookUp (context,event){
            botTrigger="1";
            var peopleUrl = "https://api.ciscospark.com/v1/people?displayName="+lookUpQuery;
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            //var body = JSON.stringify({"displayName":""+lookUpQuery});
            context.simplehttp.makeGet(peopleUrl,header,getLookUpResponse);             
        }
        function getLookUpResponse(context,event){
            var lookUpResponse = JSON.parse(event.getresp);
            for (i = 0; i < lookUpResponse.items.length; i++) {
                if(i<20){//Ensure not to flood with responses in case of vague lookup
                    var myLookUpEmail = lookUpResponse.items[i].emails[0];
                    var myLookUpName = lookUpResponse.items[i].displayName;  
                    var myLookUpAvatar = lookUpResponse.items[i].avatar;
                    if(myLookUpAvatar!=undefined || myLookUpAvatar!=null){
                        var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
                        var body = JSON.stringify({"roomId":""+roomId,"markdown":"["+myLookUpName+"](mailto:"+myLookUpEmail+")","files":""+myLookUpAvatar});
                        context.simplehttp.makePost(url,body,header); 
                    }else{
                        var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
                        var body = JSON.stringify({"roomId":""+roomId,"markdown":"["+myLookUpName+"](mailto:"+myLookUpEmail+")"});
                        context.simplehttp.makePost(url,body,header); 
                    }
                }
            }
        }
        function getPresenceResponse(context,event){
            botTrigger="1";
            var mySpark = presenceResponse.join(" \n ");
            var mySparkClean = mySpark.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+mySparkClean});
            context.simplehttp.makePost(url,body,header);  
        }
        function getBlog(context,event){
            botTrigger="1";
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":"_Responses limited to 5 most recent blog posts. For a comprehensive listing, visit the [Spark developers portal](https://developer.ciscospark.com/blog-home.html)_"});
            context.simplehttp.makePost(url,body,header);
            for (i = 0; i < blogUrl.length; i++) {
                blogTitle = blogUrl[i].substring(blogUrl[i].lastIndexOf("blog"), blogUrl[i].lastIndexOf("."));
                blogName="http://api.pdflayer.com/api/convert?access_key=7789df2fc2d8d4c607851e40822a1b42&document_url="+blogUrl[i]+"&document_name="+blogTitle;
                var body = JSON.stringify({"roomId":""+roomId,"files":""+blogName});
                context.simplehttp.makePost(url,body,header); 
            }
        }
        function getThanks(context,event){
            botTrigger="1";
            var mySpark = thanksResponse.join(" \n ");
            var mySparkClean = mySpark.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+mySparkClean});
            context.simplehttp.makePost(url,body,header);          
        }       
        function getAgeResponse(context,event){
            botTrigger="1";
            var mySpark = ageResponse.join(" \n ");
            var mySparkClean = mySpark.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+mySparkClean});
            context.simplehttp.makePost(url,body,header);          
        }
        function getWellResponse(context,event){
            botTrigger="1";
            var mySpark = wellResponse.join(" \n ");
            var mySparkClean = mySpark.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+mySparkClean});
            context.simplehttp.makePost(url,body,header);          
        }
        function getGreeting(context,event){
            botTrigger="1";
            var mySpark = greetingsResponse.join(" \n ");
            var mySparkClean = mySpark.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+mySparkClean});
            context.simplehttp.makePost(url,body,header);           
        }
        function getoverview(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            //context.sendResponse("Room ID is here: "+event.contextobj.contextid);
            //Re-create a string from an array
            var mySpark = sparkOverview.join(" \n ");
            var mySparkClean = mySpark.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+mySparkClean});
            context.simplehttp.makePost(url,body,header); 
        }
        function getdemos(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            //Re-create a string from an array
            var myDemos = partnerDemos.join(" \n ");
            var myDemosClean = myDemos.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+myDemosClean});
            //context.sendResponse(myDemosClean);
            context.simplehttp.makePost(url,body,header);   
        }
        function getExtTraining(context, event) {
            //External Training
            botTrigger="1";
            //Re-create a string from an array
            var myExtTraining = extTraining.join(" \n ");
            //Strip HTML tags from JSON response
            var myExtTrainingClean = myExtTraining.replace(regex, '');  
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+myExtTrainingClean});
            context.simplehttp.makePost(url,body,header);   
            if(domain=="cisco"){
                getIntTraining(context, event);
            }
        }
        function getIntTraining(context, event) {
            //Internal Training
            botTrigger="1";
            //Re-create a string from an array
            var myIntTraining = intTraining.join(" \n ");
            //Strip HTML tags from JSON response
            var myIntTrainingClean = myIntTraining.replace(regex, '');  
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+myIntTrainingClean});
            context.simplehttp.makePost(url,body,header);    
        }
        function getevents(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":"**For Events Request** [Submit Here](https://app.smartsheet.com/b/form?EQBCT=91b64318c7aa4afc9dbdf0489783d389)"});
            context.simplehttp.makePost(url,body,header);                     
        }
        function getDevResources(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            //Re-create a string from an array
            var myResource = devResource.join(" \n ");
            //Strip HTML tags from JSON response
            var myResourceClean = myResource.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+myResourceClean});
            context.simplehttp.makePost(url,body,header);  
        }
        function getsalesResources(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            //Internal Training
            //Re-create a string from an array
            var mySalesResource = salesResource.join(" \n ");
            var mySalesResourceClean = mySalesResource.replace(regex, '');  
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+mySalesResourceClean});
            context.simplehttp.makePost(url,body,header); 
        }
        function getcontacts(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            //Re-create a string from an array
            var myContacts = contactDetails.join(" \n ");
            var myContactsClean = myContacts.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+myContactsClean});
            context.simplehttp.makePost(url,body,header);   
        }
        function getfeedback(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            var header = {"Authorization":"Bearer NWM0OTc3OTYtMmQxMy00OGUxLWIyM2ItN2ZkN2VmZmUzNzlkOTVmMDFjMzMtMTZm","Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":"Y2lzY29zcGFyazovL3VzL1JPT00vMWJlZTg4YzAtODY0ZC0xMWU2LTlhOTMtZDE4ZjliZjNlZDAz","text":event.senderobj.display+" says " +evtMsg});
            context.simplehttp.makePost(url,body,header,sparkFeedback);
        }
        function getinthelp(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            //Re-create a string from an array
            var myIntHelp = intHelp.join(" \n ");
            //Strip HTML tags from JSON response
            var myIntHelpClean = myIntHelp.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+myIntHelpClean});
            context.simplehttp.makePost(url,body,header);
            }
        function getexthelp(context, event) {
            //Trigger to notify code a selcection have been chosen
            botTrigger="1";
            //Re-create a string from an array
            var myExtHelp = extHelp.join(" \n ");
            var myExtHelpClean = myExtHelp.replace(regex, '');                    
            var header = {"Authorization":""+sparkToken,"Content-Type": "application/json; charset=utf-8"};
            var body = JSON.stringify({"roomId":""+roomId,"markdown":""+myExtHelpClean});
            context.simplehttp.makePost(url,body,header);
        }
        function sparkFeedback(context, event) {
        //Feedback send confirmation
        context.sendResponse("Thanks for the feedback "+ event.senderobj.display+"!");
        }
        function HttpResponseHandler(context, event) {
        }
        
        function DbGetHandler(context, event) {
            context.sendResponse("testdbput keyword was last get by:" + event.dbval);
        }
    
        function DbPutHandler(context, event) {
            context.sendResponse("testdbput keyword was last put by:" + event.dbval);
        }

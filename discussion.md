<style>
*
{
	margin:0;
	padding:0;
	font font-family: tahoma,sans-serif;
	box-sizing: border-box;
}
body
{
	background:#1ddced;
	z-index: -10;
}
.chatbox
{
	width:500px;
	min-width: 390px;
	height: 400px;
	background:#fff;
	padding: 25px;
	margin:60px auto;
	box-shadow: 3px 3px #ccc;
  z-index=-1;

}
.chatlogs
{
	padding:10px;
	width:100%;
	height:450px;

}
.chat
{
	display: flex;
	flex-flow: row wrap;
	align-items: flex-start;
	margin-bottom: 40px;
}
.chat .user-photo
{
	width: 60px;
	height: 60px;
	background: #ccc;
	border-radius:50%;

}
.chat .chat-message
{
	width:80%;
	padding: 15px;
	margin:5px 10px 0;
	border-radius: 10px;
	color:#fff;
	font-size: 18px;
}
.user .chat-message
{
	background: #1adda4;
}
.bot .chat-message
{
	background:#1ddced;
	order:-1;
}
.chat-form
{
	margin-top: 100px;
	margin-left: 40px;
	display: flex;
	align-items: flex-start;
}
.chat-form input
{
	background: #fbfbfb;
	width:80%;
	height:55px;
	border:2px solid grey;
	border-radius: 5px;
	padding:10px;
	font-size: 18px;
	color: red;
}
.head
{
	background-color: black;
	color:white;
	width: 100%;
	height: 80px;
	font-size: 50px;
	padding: 10px;


}
.head p
{
	align-items: center;
	margin-left: 150px;
	text-transform: capitalize;
	
}


</style>

<script>
var trigger = [
	["hi","hey","hello"], 
	["how are you", "how is life", "how are things"],
	["what are you doing", "what is going on"],
	["how old are you"],
	["what is your task","what do you do"],
	["who are you", "are you human", "are you bot", "are you human or bot"],
	["who created you", "who made you"],
	["your name please",  "your name", "may i know your name", "what is your name"],
	["i love you"],
	["happy", "good"],
	["bad", "bored", "tired"],
	["help me", "tell me story", "tell me joke"],
	["ah", "yes", "ok", "okay", "nice", "thanks", "thank you"],
	["bye", "good bye", "goodbye", "see you later"],
	
];
var reply = [
	["Hi","Hey","Hello"], 
	["Fine", "Pretty well", "Fantastic"],
	["Nothing much", "About to go to sleep", "Can you guest?", "I don't know actually"],
	["I am 1 day old"],
	["my task is to help you out"],
	["I am just a bot", "I am a bot. What are you?"],
	[ "My God"],
	["I am nameless", "I don't have a name"],
	["I love you too", "Me too"],
	["Have you ever felt bad?", "Glad to hear it"],
	["Why?", "Why? You shouldn't!", "Try watching TV"],
	["I will", "What about?"],
	["Tell me a story", "Tell me a joke", "Tell me about yourself", "You are welcome"],
	["Bye", "Goodbye", "See you later"]

];
var alternative = ["Haha...", "Eh..."];
document.querySelector("#input").addEventListener("keypress", function(e){
	var key = e.which || e.keyCode;
	if(key === 13){ //Enter button
		var input = document.getElementById("input").value;
		document.getElementById("user").innerHTML = input;
		output(input);
	}
});
function output(input){
	try{
		var product = input + "=" + eval(input);
	} catch(e){
		var text = (input.toLowerCase()).replace(/[^\w\s\d]/gi, ""); //remove all chars except words, space and 
		text = text.replace(/ a /g, " ").replace(/i feel /g, "").replace(/whats/g, "what is").replace(/please /g, "").replace(/ please/g, "");
		if(compare(trigger, reply, text)){
			var product = compare(trigger, reply, text);
		} else {
			var product = alternative[Math.floor(Math.random()*alternative.length)];
		}
	}
	document.getElementById("chatbot").innerHTML = product;
	
	document.getElementById("input").value = ""; //clear input value
}
function compare(arr, array, string){
	var item;
	for(var x=0; x<arr.length; x++){
		for(var y=0; y<array.length; y++){
			if(arr[x][y] == string){
				items = array[x];
				item =  items[Math.floor(Math.random()*items.length)];
			}
		}
	}
	return item;
}
</script>

<html>
<head>
	<title>chatbot</title>
	<link rel="stylesheet" type="text/css" href="style.css">
	<link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Allerta+Stencil">
</head>
<body>
    <div class="head">
    	<p >a simple chatbot</p>
    </div>
<div class="chatbox">
	<div class="chatlogs">
		<div class="chat user">
			<div class="user-photo"></div>
                 <div class="chat-message">user: <span id="user"></span></div>
             </div>
	<div class="chat bot">
		<div class="user-photo"></div>
	<div class="chat-message">chatbot: <span id="chatbot"></span></div>
	</div>
	<div class="chat-form"><input id="input" type="text" placeholder="say anything..." autocomplete="off"/></div>
<script type="text/javascript" src="script.js"></script>	
</div>
</body>
</html>
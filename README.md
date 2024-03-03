# Internsrmyproject
Design a web application “Web-Based Chat Application” to allow users to chat with each other.
#
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <title>Tuts+ Chat Application</title>
    <meta name="description" content="Tuts+ Chat Application" />
    <link rel="stylesheet" href="style.css" />
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
</head>
<body>
    <div id="wrapper">
        <div id="menu">
            <p class="welcome">Welcome, <b></b></p>
            <p class="logout"><a id="exit" href="#">Exit Chat</a></p>
        </div>

        <div id="chatbox"></div>

        <form name="message" action="">
            <input name="usermsg" type="text" id="usermsg" />
            <input name="submitmsg" type="submit" id="submitmsg" value="Send" />
        </form>
    </div>

    <script type="text/javascript" src="script.js"></script>
</body>
</html>

CSS


* {
    margin: 0;
    padding: 0;
}

#wrapper {
    width: 1000px;
    height: 600px;
    border: 1px solid black;
    margin: 0 auto;
    padding: 10px;
}

#menu {
    padding: 15px 25px;
    display: flex;
}

#menu p.welcome {
    flex: 1;
}

a#exit {
    color: white;
    background: #c62828;
    padding: 4px 8px;
    border-radius: 4px;
    font-weight: bold;
}

#chatbox {
    height: 460px;
    border: 1px solid black;
    padding: 10px;
    overflow: scroll;
}

.msgln {
    margin: 0 0 5px 0;
}

.msgln span.left-info {
    float: left;
}

.msgln span.right-info {
    float: right;
}

.msgln div.msg-content {
    padding: 3px 10px;
    border: 1px solid black;
    border-radius: 10px;
    max-width: 80%;
}

.msgln div.msg-content.left {
    float: left;
    background: #ddd;
}

.msgln div.msg-content.right {
    float: right;
    background: #4CAF50;
    color: white;
}


Js

$(document).ready(function () {
    var username = '';
    var typing = false;
    var timeout = undefined;

    // Function to handle form submission
    $('#message').submit(function (e) {
        e.preventDefault();
        sendMessage();
    });

    // Function to send a message
    function sendMessage() {
        var msg = $('#usermsg').val();
        if (msg !== '') {
            $('#usermsg').val('');
            $.post('post.php', {text: msg, username: username}, function () {
            });
        }
    }

    // Function to handle typing
    $('#usermsg').on('input', function () {
        username = $('.welcome b').text();
        if (username !== '') {
            typing = true;
            socket.emit('typing', {username: username});
        }
        clearTimeout(timeout);



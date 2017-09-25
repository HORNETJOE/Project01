# Product Backlog

# Sprint Backlog

<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<style>
canvas {
    border:1px solid #d3d3d3;
    background-color: #f1f1f1;
}
</style>
</head>
<body onload="startGame()">
<script>

var myGamePiece;
var targetPiece;
var gamepieceX;
gamepieceX = 30;
gamepieceY = 30;
var othergamepieceX;
var othergamepieceY;
othergamepieceX = 100;
othergamepieceY = 100;
var gamelives;
gamelives = 3;
document.write(gamelives ," lives left")

function startGame() {
    myGamePiece = new component(30, 30, "red", gamepieceX, gamepieceY);
    targetPiece = new component(30, 30, "blue", othergamepieceX,othergamepieceY);
    
    myGameArea.start();
}

var myGameArea = {
    canvas : document.createElement("canvas"),
    start : function() {
        this.canvas.width = 480;
        this.canvas.height = 270;
        this.context = this.canvas.getContext("2d");
        document.body.insertBefore(this.canvas, document.body.childNodes[0]);
        this.interval = setInterval(updateGameArea, 20);
		window.addEventListener('mousemove', function (e) {
			myGameArea.x = e.pageX;
			myGameArea.y = e.pageY;
		})
    },
    clear : function() {
        this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
    }
}

function component(width, height, color, x, y) {
    this.width = width;
    this.height = height;
	this.speedX = 0;
	this.speedY = 0; 
	this.x = x;
	this.y = y;
    this.update = function(){
        ctx = myGameArea.context;
        ctx.fillStyle = color;
        ctx.fillRect(this.x, this.y, this.width, this.height);
    }
}

function updateGameArea() {
    myGameArea.clear();
	if (myGameArea.x && myGameArea.y) {
		targetPiece.x = myGameArea.x;
		targetPiece.y = myGameArea.y;
	}
	othergamepieceX = targetPiece.x
	othergamepieceY = targetPiece.y
	myGamePiece.update();
    targetPiece.update();
	
    //document.write(gamepieceX)
    if (myGamePiece.x < othergamepieceX) {
    	myGamePiece.x += 1;
		targetPiece.update();
		myGamePiece.update();
	}
	if (myGamePiece.x > othergamepieceX) {
    	myGamePiece.x -= 1;
		targetPiece.update();
		myGamePiece.update();
	}
	
	
	if (myGamePiece.y < othergamepieceY) {
    	myGamePiece.y += 1;
		targetPiece.update();
		myGamePiece.update();
	}
	
	if (myGamePiece.y > othergamepieceY) {
    	myGamePiece.y -= 1;
		targetPiece.update();
		myGamePiece.update();
	}
	
	if (myGamePiece.y == othergamepieceY && myGamePiece.x == othergamepieceX) {
		myGamePiece.y = 30;
		myGamePiece.x = 30;
		gamelives = gamelives - 1;
		//document.write(gamelives ," lives left")
	}
	
	if (gamelives == 0) {
		document.write("GameOver");
		endgame.start();
	}
   
}
function endgame(){
	document.write(gamelives)
	break;
}

</script>
</body>
</html>

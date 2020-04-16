<html>
<head>
    <meta charset="utf-8" />
    <title>WordWorld</title>
    <style>
     * { padding: 0; margin: 0; }
     canvas { background: #eee; display: block; margin: 0 auto; }
    </style>
</head>
<body>

<canvas id="myCanvas" width="800" height="800"></canvas>



<script>
var base_width = 800;
var base_height = 40;
var base_x = 0;
var base_y = myCanvas.height - base_height;
var canvas = document.getElementById("myCanvas");
var ctx = canvas.getContext("2d");
var wordcycletime = 500;
var dx = 1.9;
var dy = 1.9;
var difficulty = 0.7
var deltatime = 0.0001;
var x = 0;
var y = 0;
var time = 0;
var words = [];
var touchpressed = [];
var score = 500;
var chaintext = "";
var game = false;
var mousepositionX;
var mousepositionY;
var mouseclickpositionX = 0;
var mouseclickpositionY = 0;
var audio = new Audio('son.mp3');
var currentTime = 0;
var backgroundImage = new Image();
var gameover = false;
backgroundImage.src = 'img_background_menu.jpeg';




var bt_gameover = [];

bt_gameover[0] = {texte : "Revenir au menu", positionX : canvas.width/2-150, positionY : canvas.height/2+50, largeur : 300, hauteur : 50, activate : false};

var bt_menu = [];

bt_menu[0] = {texte : "Play", positionX : canvas.width/2-150, positionY : canvas.height/2-200, largeur : 300, hauteur : 50, activate : false};

 touchpressed[0] =  {touch :  "a", keyDown : false};
 touchpressed[1] =  {touch :  "b", keyDown : false};
 touchpressed[2] =  {touch :  "c", keyDown : false};
 touchpressed[3] =  {touch :  "d", keyDown : false};
 touchpressed[4] =  {touch :  "e", keyDown : false};
 touchpressed[5] =  {touch :  "f", keyDown : false};
 touchpressed[6] =  {touch :  "g", keyDown : false};
 touchpressed[7] =  {touch :  "h", keyDown : false};
touchpressed[8] =  {touch :  "i", keyDown : false};
touchpressed[9] =  {touch :  "j", keyDown : false};
touchpressed[10] = {touch : "k", keyDown : false};
touchpressed[11] = {touch :  "l", keyDown : false};
touchpressed[12] = {touch :  "m", keyDown : false};
touchpressed[13] = {touch :  "n", keyDown : false};
touchpressed[14] = {touch :  "o", keyDown : false};
touchpressed[15] = {touch :  "p", keyDown : false};
touchpressed[16] = {touch :  "q", keyDown : false};
touchpressed[17] = {touch :  "r", keyDown : false};
touchpressed[18] = {touch :  "s", keyDown : false};
touchpressed[19] = {touch :  "t", keyDown : false};
touchpressed[20] = {touch :  "u", keyDown : false};
touchpressed[21] = {touch :  "v", keyDown : false};
touchpressed[22] = {touch :  "w", keyDown : false};
touchpressed[23] = {touch :  "x", keyDown : false};
touchpressed[24] = {touch :  "y", keyDown : false};
touchpressed[25] = {touch :  "z", keyDown : false};

document.addEventListener("keydown", keyDownHandler, false);
document.addEventListener("keyup", keyUpHandler, false);
document.addEventListener("mousemove", mouseMoveHandler, false);
document.addEventListener("click", mouseClick, false);


words[0] = {fr: "a", en: "a", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[1] = {fr: "b", en: "b", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[2] = {fr: "c", en: "c", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[3] = {fr: "d", en: "d", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[4] = {fr: "e", en: "e", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[5] = {fr: "f", en: "f", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[6] = {fr: "g", en: "g", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[7] = {fr: "h", en: "h", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[8] = {fr: "i", en: "i", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[9] = {fr: "j", en: "j", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[10] = {fr: "k", en: "k", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[11] = {fr: "l", en: "l", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[12] = {fr: "m", en: "m", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[13] = {fr: "n", en: "n", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[14] = {fr: "o", en: "o", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[15] = {fr: "p", en: "p", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[16] = {fr: "q", en: "q", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[17] = {fr: "r", en: "r", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};
words[18] = {fr: "s", en: "s", statut : false, positionX : 0, positionY : 0, anciennepositionX : 0, anciennepositionY : 0, dx : 0.5+difficulty, dy : 0.5+difficulty, timelastcrash : 0, statutcrash : false};



function mouseMoveHandler(e) {

mousepositionX = e.clientX - canvas.offsetLeft;
mousepositionY = e.clientY - canvas.offsetTop;


}


function reinitialisation (){

for (i = 0; i <words.length; i++) {

words[i].positionX = 0;
words[i].positionY = 0;
words[i].anciennepositionX = 0;
words[i].anciennepositionY = 0;

}


score = 500;
deltatime = 0,01;
}

function mouseClick(e) {

mouseclickpositionX = e.clientX - canvas.offsetLeft;
mouseclickpositionY = e.clientY;
console.log("Mouseposition X = " + mousepositionX);
console.log("Prenant comptant d'un decalage gauche de" + canvas.offsetLeft);
console.log("Mouseposition X = " + mousepositionY);
console.log("Prenant comptant d'un decalage haut de" + canvas.offsetTop);


}

function eventMenu () {

a = false; 


if ((((mouseclickpositionX < bt_menu[0].positionX) || (mouseclickpositionX > bt_menu[0].positionX+bt_menu[0].largeur))  || ((mouseclickpositionY < bt_menu[0].positionY) || (mouseclickpositionY >  bt_menu[0].positionY + bt_menu[0].hauteur)))) {

}
else {


game = true;
gameover = false;
a = true;
}

if ((((mouseclickpositionX < bt_gameover[0].positionX) || (mouseclickpositionX > bt_gameover[0].positionX+bt_gameover[0].largeur))  || ((mouseclickpositionY < bt_gameover[0].positionY) || (mouseclickpositionY >  bt_gameover[0].positionY + bt_gameover[0].hauteur)))) {

}
else {


gameover = false;
game = false;
a = true;

}

if (a == true)
{ return true;
}
else {
return false;}


}

function keyDownHandler (e)
{

for (i = 65; i <= 90; i++) {

if (i == e.keyCode) {

touchpressed[i-65].keyDown = true;

}


}

if (e.keyCode == 8)
{

chaintext = chaintext.substring(0, chaintext.length - 1);

}

if (e.keyCode == 13)
{

	for (i = 0; i <words.length; i++) {
	
		if (chaintext == words[i].en) {
		chaintext = "";
		words[i].statut = false;
		
		}
	}
	
}

}

function keyUpHandler (e)
{

for (i = 65; i <= 90; i++) {

if (i == e.keyCode) {
//alert(e.keyCode);
touchpressed[i-65].keyDown = false;
break;
}

}
}


function draw_score () {
ctx.fillText("score " + score, 15, 25);

}

function losspoint () {

score--

}

function collision () {

// verif si perte
for (i = 0; i <words.length; i++) {

	if (words[i].positionY >= base_y) {
		words[i].statut = false;
		words[i].positionY = 0;
		//currentTime = audio.currentTime;
		audio2 = new Audio('explosion.mp3');
		audio2.play();
		//setTimeout(audio.pause(), 1000);
		
		//do {
		//console.log("boucle");
		//}while(audio.paused== false) 
		var audio = new Audio('son.mp3');
		losspoint();
	}
	}

} 


function draw_menu () {

ctx.drawImage(backgroundImage, 0,0,canvas.width, canvas.height );

if (((mousepositionX < bt_menu[0].positionX) || (mousepositionX > bt_menu[0].positionX+bt_menu[0].largeur))  || ((mousepositionY < bt_menu[0].positionY) || (mousepositionY >  bt_menu[0].positionY + bt_menu[0].hauteur))) {
	ctx.fillStyle = 'rgb(233, 176, 10)';
	ctx.lineWidth = 3;
	ctx.fillRect(bt_menu[0].positionX, bt_menu[0].positionY, bt_menu[0].largeur, bt_menu[0].hauteur);
	ctx.font = "20px Arial";
	ctx.fillStyle = 'rgb(120, 115, 0)';
	ctx.fillText(bt_menu[0].texte, bt_menu[0].positionX+bt_menu[0].largeur/2-bt_menu[0].texte.length*5, bt_menu[0].positionY+bt_menu[0].hauteur/2+bt_menu[0].texte.length*2);
//	console.log(mousepositionXt+ " " + mousepositionY);
	
} 
else {
	ctx.fillStyle = 'rgb(230, 155, 49)';
	ctx.lineWidth = 1;
	ctx.fillRect(bt_menu[0].positionX, bt_menu[0].positionY, bt_menu[0].largeur,  bt_menu[0].hauteur);
	ctx.font = "20px Arial";
	ctx.fillStyle = 'rgb(120, 115, 0)';
	ctx.fillText(bt_menu[0].texte, bt_menu[0].positionX+bt_menu[0].largeur/2-bt_menu[0].texte.length*5, bt_menu[0].positionY+bt_menu[0].hauteur/2+bt_menu[0].texte.length*2);

}


}
function draw_base (){

ctx.beginPath();
ctx.rect(base_x, base_y, base_width, base_height);
ctx.stroke();

}

function generate_new_word () {

if (Math.random() >= 0.985-deltatime) {

return true;
}

deltatime = deltatime*2;
}

function draw_write () {

for (i = 0; i <26; i++) {

if (touchpressed[i].keyDown == true) {
//console.log("ecriturelettre");
chaintext = chaintext + touchpressed[i].touch;
ctx.fillText(chaintext, canvas.width / 2, canvas.height-20);
touchpressed[i].keyDown = false;

}
else ctx.fillText(chaintext, canvas.width / 2, canvas.height-20);

}




}

function draw_gameover () {

ctx.font = "80px Arial";
ctx.fillText("GAME OVER", canvas.width / 2 - 9 * 25, canvas.height/2);

if (((mousepositionX < bt_gameover[0].positionX) || (mousepositionX > bt_gameover[0].positionX+bt_gameover[0].largeur))  || ((mousepositionY < bt_gameover[0].positionY) || (mousepositionY >  bt_gameover[0].positionY + bt_gameover[0].hauteur))) {
	ctx.fillStyle = 'rgb(233, 176, 10)';
	ctx.lineWidth = 3;
	ctx.fillRect(bt_gameover[0].positionX, bt_gameover[0].positionY, bt_gameover[0].largeur, bt_gameover[0].hauteur);
	ctx.font = "20px Arial";
	ctx.fillStyle = 'rgb(120, 115, 0)';
	ctx.fillText(bt_gameover[0].texte, bt_gameover[0].positionX+bt_gameover[0].largeur/2-bt_gameover[0].texte.length*5, bt_gameover[0].positionY+bt_gameover[0].hauteur/2+3);
//	console.log(mousepositionXt+ " " + mousepositionY);
	
} 
else {
	ctx.fillStyle = 'rgb(230, 155, 49)';
	ctx.lineWidth = 1;
	ctx.fillRect(bt_gameover[0].positionX, bt_gameover[0].positionY, bt_gameover[0].largeur,  bt_gameover[0].hauteur);
	ctx.font = "20px Arial";
	ctx.fillStyle = 'rgb(120, 115, 0)';
	ctx.fillText(bt_gameover[0].texte, bt_gameover[0].positionX+bt_gameover[0].largeur/2-bt_gameover[0].texte.length*5, bt_gameover[0].positionY+bt_gameover[0].hauteur/2+3);

}


}



function draw_word () 
{

ctx.font = "18px Arial";

if (generate_new_word())
{
	do 
	p = Math.floor(Math.random() * words.length)
	while (words[p].statut == true)
	words[p].statut = true;
	words[p].positionX = Math.floor(Math.random() * canvas.width);
	words[p].positionY = 0;
}


for ( i = 0;  i < words.length; i++) {
	if (words[i].statut == true) {
			ctx.fillText(words[i].fr, words[i].positionX, words[i].positionY);
			if (words[i].positionX > canvas.width - words[i].fr.length * 2) 	{
				words[i].dx = dx;
			}
			if (words[i].positionX <= 0 ) 	{
				words[i].dx = -dx
			}
			
		for ( j = 0;  j < words.length; j++) {
			if (j !=i && words[j].statut == true) {
								
				if (
					(words[i].positionX >= words[j].positionX - 30) &&
					(words[i].positionX <= words[j].positionX + 30) &&
					(words[i].positionY >= words[j].positionY - 30) && 
					(words[i].positionY <= words[j].positionY + 30) 					
					){ 
	
						if (words[i].dx < 0 && words[i].statutcrash == false ) {
							words[i].dx = dx;
							words[j].dx = -dx;
							words[i].statutcrash = true;
							
						}
						
						else if (words[i].dx > 0 && words[i].statutcrash == false) {
					
							words[i].dx = -dx; 
							words[j].dx = dx;
			
							words[i].statutcrash = true;
						}
				}
				
				if (words[i].statutcrash ==true) {
					words[i].timelastcrash ++;
				}
				if (words[i].timelastcrash >= 900) { 
								words[i].statutcrash = false;
								words[i].timelastcrash = 0;
				}
			}
		}
	}
}






for ( i = 0;  i < words.length; i++) {
		if (words[i].statut == true) {   
		ctx.fillText(words[i].fr, words[i].positionX, words[i].positionY);
				if (words[i].positionX > canvas.width - words[i].fr.length * 2) 	{
				words[i].dx = -dx;
				}
				if (words[i].positionX <= 0 ) 	{
				words[i].dx = dx;
				}

		}
	}

}



function draw ()

{

if (game == true && gameover == false) {
	if (score >0) {
		ctx.clearRect(0, 0, canvas.width, canvas.height);
		draw_base();
		draw_word();
		draw_write();
		collision();
		draw_score();
		audio.play();
		time = time + 1;
		for ( i = 0;  i < words.length; i++) {
			if (words[i].statut == true) {   
				words[i].positionX = words[i].positionX + words[i].dx;
				words[i].positionY = words[i].positionY + words[i].dy;
			}
		}
	}

	else  {
		gameover = true;

	}
}

else if (game == true && gameover == true){
draw_gameover();
eventMenu();

}
else {

game = false;
gameover = false;
draw_menu();
eventMenu();
reinitialisation();


}
}



var interval = setInterval(draw, 10);

</script>

</body>
</html>

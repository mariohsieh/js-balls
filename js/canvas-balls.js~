window.onload = function() {
	// declare and initialize variables
	var ctx;
	var gravity = 4;
	var forceFactor = 0.3;
	var mouseDown = false;
	var balls = [];
	var mousePos = [];


	// event handlers
	function onMouseDown(evt) {
		mouseDown = true;
		mousePos['downX'] = evt.pageX;
		mousePos['downY'] = evt.pageY;
	}

	function onMouseUp(evt) {
		mouseDown = false;
		velX = (evt.pageX - mousePos['downX']) * forceFactor;	// calc velocity x-value
		velY = (evt.pageY - mousePos['downY']) * forceFactor;	// calc velocity x-value
		rad = 5+(Math.random()*10);	// calc radius

		balls.push(new ball(mousePos['downX'], mousePos['downY'], velX, velY, rad, 0.9, random_color()));
	}

	function onMouseMove(evt) {
		mousePos['currentX'] = evt.pageX;
		mousePos['currentY'] = evt.pageY;
	}

	function resizeWindow(evt) {
		canvas.height = $(window).height();
		canvas.width = $(window).width();
	}

	$(document).mousedown(onMouseDown);
	$(document).mouseup(onMouseUp);
	$(document).mousemove(onMouseMove);
	$(window).bind("resize", resizeWindow);

	//// graphics code ////

	//	draw a circle
	function circle(x, y, r, c) {
		ctx.beginPath();
		ctx.arc(x, y, r, 0, Math.PI*2, true);
		ctx.closePath();
		// fill path
		ctx.fillStyle = c;
		ctx.fill();
		// stroke
		ctx.lineWidth = r * 0.1;
		ctx.strokeStyle = "#000000";
		ctx.stroke();
	}

	//	give each circle a random color
	function random_color() {
		var letter = "0123456789ABCDEF".split("");	// all possible color combinations
		var color = "#";
		for (var i = 0; i < 6; i++) {
			color += letter[Math.round(Math.random()*15)];	
		}
		return color;
	}


	function arrow(fromX, fromY, toX, toY, c) {
		ctx.beginPath();
		var headlen = 10;
		var angle = Math.atan2(toY-fromY, toX-fromX);
		ctx.moveTo(fromX, fromY);
		ctx.lineTo(toX, toY);
		ctx.lineTo(toX-headlen*Math.cos(angle-Math.PI/6), toY-headlen*Math.sin(angle-Math.PI/6));
		ctx.moveTo(toX, toY);
		ctx.lineTo(toX-headlen*Math.cos(angle+Math.PI/6), toY-headlen*Math.sin(angle+Math.PI/6));

		//style
		ctx.lineWidth = 1;
		ctx.strokeStyle = c;
		ctx.lineCap = "butt";
		ctx.stroke();
	}


	function draw_ball() {
		// apply gravity
		this.vy += gravity * 0.1;	// v = a * t
		this.x += this.vx * 0.1;	// s = v * t
		this.y += this.vy * 0.1;	
		
		// collision with walls
		if (this.x + this.r > canvas.width) {	// right border
			this.x = canvas.width - this.r;
			this.vx *= -1 * this.b;
		}

		if (this.x - this.r < 0) {	// left border
			this.x = this.r;
			this.vx *= -1 * this.b;
		}

		if (this.y + this.r > canvas.height) {	// bottom border
			this.y = canvas.height - this.r;
			this.vy *= -1 * this.b;
		}

		if (this.y - this.r < 0) {	// top border
			this.y = this.r;
			this.vy *= -1 * this.b;
		}

		circle(this.x, this.y, this.r, this.c);
	}

	////	objects ////
	function ball(positionX, positionY, velocityX, velocityY, radius, bounciness, color) {
		this.x = positionX;
		this.y = positionY;
		this.vx = velocityX;
		this.vy = velocityY;
		this.r = radius;
		this.b = bounciness;
		this.c = color;

		this.draw = draw_ball;
	}


	//// game loop ////
	function game_loop() {
		ctx.clearRect(0, 0, canvas.width, canvas.height);	// clear screen each time it runs

		if (mouseDown == true) {
			arrow(mousePos['downX'], mousePos['downY'], mousePos['currentX'], mousePos['currentY'], "red");
		}

		for (var i = 0; i < balls.length; i++) {
			balls[i].draw();
		}

		ctx.fillStyle = "#000000";
		ctx.font = "15px Arial";
		ctx.fillText("Balls: " + balls.length, 10, canvas.height - 10);
	}



	//// game start! ////
	function init() {
		ctx = $('#canvas')[0].getContext("2d");
		canvas.height = $(window).height();
		canvas.width = $(window).width();
		return setInterval(game_loop, 10)
	}

	init();
}

























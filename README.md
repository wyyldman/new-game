# new-gameecho "# new-game" >> README.md<!DOCTYPE html>
<html>
	<title>Fantasy Tank Builder</title>
	<head>
		<link rel="stylesheet" href="styles.css">
		<link href="https://fonts.googleapis.com/css?family=Ubuntu" rel="stylesheet">
	</head>
	<body onload="onload()">
		<canvas id="game"></canvas>
		<script src="scripts/globals.js"></script>
		<script src="scripts/drawBackground.js"></script>
		<script src="scripts/drawGraphics.js"></script>
		<script src="scripts/gameController.js"></script>
		
		<p id="watermark">Play at iblobtouch.github.io!</p>
		
		<p id="spawnlabel" >Spawn shapes?</p>
		<input type="checkbox" id="spawn">
		
		<button id = "editbutton" onclick = "editButtonClick()">Toggle edit mode.</button>
		<button class="editbuttons" id = "bodybutton" onclick = "bodyClick()">Body/Color settings</button>
		<button class="editbuttons" id = "barrelbutton" onclick = "barrelClick()">Barrel settings</button>
		<button class="editbuttons" id = "bulletbutton" onclick = "bulletClick()">Bullet settings</button>
		<button class="editbuttons" id = "savebutton" onclick = "saveClick()">Export/Import</button>
		
		<p id = "note">Press the edit mode button to edit the tank. <br> Press e to autofire and c to autospin. <br> Refresh the page to get a new tank.</p>
		
		<p class="editbuttons tanksettings pos1label">Radius <span title="Specifies the radius of the tank's main body." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons tanksettings pos1" id = "body" rows="1" cols = "10" placeholder = "Body Size" title="Specifies the radius of the tank's main body.">32</textarea>
		
		<p class="editbuttons tanksettings pos2label">Body <span title="Specifies the type of body should be used." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<select class = "editbuttons tanksettings pos2" id = "shape" title="Specifies the type of body should be used.">
			<option value="circle">Circle</option> 
  			<option value="square">Square</option>
  			<option value="smasher">Smasher</option>
			<option value="triangle">Triangle</option>
			<option value="pentagon">Pentagon</option>
			<option value="mothership">Mothership</option>
		</select>
		
		<p class="editbuttons tanksettings pos3label">Colour <span title="Specifies what colour should be used for the tank and bullets." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<input type = "color" class="editbuttons tanksettings pos3" id = "color" value = "#00B2E1" title="Specifies what colour should be used for the tank and bullets.">
		
		<p class="editbuttons tanksettings pos4label" >Invisibility <span title="Toggles fadeout invisibility for tanks. WARNING: Dos not save to export. Yet." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<input type="checkbox" class = "editbuttons tanksettings pos4" id="invis" title="Toggles fadeout invisibility for tanks. WARNING: Dos not save to export. Yet.">
		
		<p class="editbuttons tanksettings pos5label">Drone Limit <span title="Specifies the maximum number of drones that can be on screen." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons tanksettings pos5" id = "drones" rows="1" cols = "10" placeholder = "Max Drones" title="Specifies the maximum number of drones that can be on screen.">8</textarea>
		
		<p class="editbuttons tanksettings pos6label">Necro Drone Limit <span title="Specifies the maximum number of Necromancer type drones that can be on screen." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons tanksettings pos6" id = "necrodrones" rows="1" cols = "10" placeholder = "Max Drones" title="Specifies the maximum number of Necromancer type drones that can be on screen.">16</textarea>
		
		<p class="editbuttons barrelsettings pos1label" id = "traplabel" >Barrel <span title="Specifies what type of barrel you want to place." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<select class = "editbuttons barrelsettings pos1" id = "bullet" title="Specifies what type of barrel you want to place.">
			<option value="bullet">Gun</option> 
  			<option value="trap">Trap Layer</option>
  			<option value="drone">Drone Maker</option>
			<option value="necro">Sunchips!</option>
		</select>
		
		<p class="editbuttons barrelsettings pos2label">Can Shoot? <span title="Toggles this cannon's ability to shoot." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<input type="checkbox" class = "editbuttons barrelsettings pos2" id="disable" checked title="Toggles this cannon's ability to shoot.">
		
		<p class="editbuttons barrelsettings pos3label">Width <span title="Specifies the width of the cannon." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos3" id = "width" rows="1" cols = "10"  placeholder = "width" title="Specifies the width of the cannon.">15</textarea>
		
		<p class="editbuttons barrelsettings pos4label">Length <span title="Specifies the length of the cannon." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos4" id = "length" rows="1" cols = "10"  placeholder = "length" title="Specifies the length of the cannon.">60</textarea>
		
		<p class="editbuttons barrelsettings pos5label">X Offset <span title="Specifies the distance above or below the center. Negative values moves to the right, positive to the left." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos5" id = "offset" rows="1" cols = "10"  placeholder = "offset" title="Specifies the distance above or below the center. Negative values moves to the right, positive to the left.">0</textarea>
		
		<p class="editbuttons barrelsettings pos6label">Y Offset <span title="Specifies the distance from the center of the tank. Negative values moves down, positive moves up." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos6" id = "offsetx" rows="1" cols = "10"  placeholder = "offset" title="Specifies the distance from the center of the tank. Negative values moves down, positive moves up.">0</textarea>
		
		<p class="editbuttons barrelsettings pos7label">Reload <span title="Specifies the time it takes to fire again, in seconds." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos7" id = "reload" rows="1" cols = "10"  placeholder = "Reload" title="Specifies the time it takes to fire again, in seconds.">2</textarea>
		
		<p class="editbuttons barrelsettings pos8label">Recoil <span title="Specifies how much recoil/knockback this cannon gives." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos8" id = "knockback" rows="1" cols = "10"  placeholder = "Knockback" title="Specifies how much recoil/knockback this cannon gives.">0</textarea>
		
		<p class="editbuttons barrelsettings pos9label">Spread <span title="Specifies the accuracy of this cannon in degrees. 0 = Fires in a straight line. 360 = fires randomly in any direction. Recommended values are between 0-30." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos9" id = "spread" rows="1" cols = "10"  placeholder = "Knockback" title="Specifies the accuracy of this cannon in degrees. 0 = Fires in a straight line. 360 = fires randomly in any direction. Recommended values are between 0-30.">0</textarea>
		
		<p class="editbuttons barrelsettings pos10label">Bullet Damage <span title="Specifies the damage of the bullets this cannon fires. Squares = 100HP  Triangles = 300HP  Pentagons = 1400HP" style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons barrelsettings pos10" id = "damage" rows="1" cols = "10"  placeholder = "length" title="Specifies the damage of the bullets this cannon fires. Squares = 100HP  Triangles = 300HP  Pentagons = 1400HP">65</textarea>
		
		<p class="editbuttons bulletsettings pos1label">Bullet Size <span title="Specifies the size of the projectiles this cannon fires." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons bulletsettings pos1" id = "size" rows="1" cols = "10"  placeholder = "width" title="Specifies the size of the projectiles this cannon fires.">15</textarea>
		
		<p class="editbuttons bulletsettings pos2label">Bullet Speed <span title="Specifies the speed of the projectiles this cannon fires." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons bulletsettings pos2" id = "speed" rows="1" cols = "10"  placeholder = "width" title="Specifies the speed of the projectiles this cannon fires.">50</textarea>
		
		<p class="editbuttons bulletsettings pos3label">Bullet Lifespan <span title="Specifies the lifetime of the projectiles this cannon fires. Does not effect drones. Value is in seconds." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<textarea class="editbuttons bulletsettings pos3" id = "time" rows="1" cols = "10"  placeholder = "length" title="Specifies the lifetime of the projectiles this cannon fires. Does not effect drones. Value is in seconds.">1</textarea>
		
		<p class="editbuttons bulletsettings pos4label">Toggle Inherit <span title="Toggles if these values are ignored by the barrel. Uncheck to use these values." style="color:#0022C8;text-decoration:none;">[i]</span></p>
		<input type="checkbox" class = "editbuttons bulletsettings pos4" id="use" checked title="Toggles if these values are ignored by the barrel. Uncheck to use these values.">
		
		<button class = "editbuttons savesettings pos1label" onclick = "printObject()" >Export tank.</button>
		<button class = "editbuttons savesettings " style = "margin-left: 100px; margin-top: 10px;" onclick = "importObject()" >Import tank.</button>
		<textarea class="editbuttons savesettings pos1" id = "save" rows="10" cols = "56"  placeholder = "Save Codes go here..." style = "resize: both" ></textarea>
		
		<p class="editbuttons" id = "notes">Pressing q also places a barrel. Remeber to click outside any of the boxes before doing this so you don't type q in there! <br> Press F while a placed barrel is selected to delete it.<br> Ctrl + scrollWheel to increase/decrease FOV. <br> Red line shows where the tank will be facing outside of edit mode. <br> Hold shift to rotate the barrel in 15° increments.<br> Note that guns are drawn in order of last placed to first.</p>
	</body>

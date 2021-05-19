var score = 0;
var fruitGroup = createGroup(); 
var bombGroup = createGroup(); 
var sword;
var count;
var bomb;
var ground = createSprite(200,200,400,20);
ground.setAnimation("h");

// Game State 
var PLAY = 1;
var END = 0;
var gameState = 1;
console.log(gameState);
var fruits = createSprite();

function draw() {
 background("white");
 
 if (fruitGroup.isTouching(sword)){
  fruitGroup.destroyEach();
  score=score+2;
}





 
   if(gameState === PLAY){
    //move the ground
    //scoring
    count = Math.round(World.frameCount/4);
   if(count % 100 === 0 && count > 0){
     
    //add gravity
    fruits.velocityY = sword.velocityY + 0.8;
    
    //End the game when sword is touching the Bomb
    if(bombGroup.isTouching(sword)){
      gameState = END;
     
//Code for the Sword to work in Game Starts
 sword.setAnimation("sword");
 sword.x=200;
 sword.y=200;
 sword.y=World.mouseY;
 sword.x=World.mouseX;
 
//Code for the Bomb AKA "Enemy"
  if(World.frameCount%200===0){
    var monster=createSprite(400,200,20,20);
    monster.setAnimation("alienGreen_badge_1");
    monster.y=randomNumber(100,300);
    monster.velocityX=-8;
    monster.setLifetime=50;
    bombGroup.add(monster);
    bomb(); 


  if(World.frameCount%80===0) {
    var fruit=createSprite(400,200,20,20);
    fruit.scale=0.2;
    //fruit.debug=true;
    var r=randomNumber(1,4);
    fruit.setAnimation("fruit"+r);
    fruit.y=randomNumber(50,340);
    fruit.velocityX=-7;
    fruit.setLifetime=100;
    fruitGroup.add(fruits);
    fruits();

  }
}
    }
  }
  
  else if(gameState === END) {
    //set velcity of each game object to 0
    ground.velocityX = 0;
    sword.velocityY = 0;
    bombGroup.setVelocityXEach(0);
   
    
    //set lifetime of the game bomb so that they are never destroyed
    bombGroup.setLifetimeEach(-1);
    
    
    //place gameOver and restart icon on the screen
    var gameOver = createSprite(200,300);
    var restart = createSprite(200,340);
    
    gameOver.setAnimation("GO");
    gameOver.scale = 0.5;
    restart.setAnimation("R");
    restart.scale = 0.5;
  }
}
 
 drawSprites();
}

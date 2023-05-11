## Introduction
This practical work is delivery document for class of Video Game Development Techniques of the course of Engineering in Digital Game Development, proposed by Professor Daniel Nogueira. The work has several tasks and objectives given by teacher:
* A brief description of the game.
* Decisions made in development of game.
* The game instructions.
* Brief analysis and Organization of the files and code.

# The game "[FlappyBird](https://github.com/SongToSoft/FlappyBird/tree/master/FlappyBird/FlappyBird)"
![](https://image.cnbcfm.com/api/v1/image/101508108-flappy_bird.jpg?v=1395251000&w=740&h=416&ffmt=webp&vtcrop=y)

I’m going to analyze this game on basis of tasks given by teacher and i chose  this  game for this purpose  because  Its open source, simple and easy to understand for beginners and It doesn’t have complex  UI/UX.

## Introduction
Flappy bird is an arcade-style game which follow the pixelated bird called 'Faby' and is controlled by user.Goal is to fly between as many pipes as you can without getting hit

## Mechanism 
Game mechanism is to create an addictive hit. Tapping the space button ‘lift’ to the main character, which is used strategically to navigate through a series of moving pipes and then a  point is scored for each pipe successfully passed. 

## Instructions 
The instruction for this  game  are v ery  simple. Press the spacebar to allow your bird to fly and to start the  game. Stay in the middle of screen until  the  first set of pipes appears. Measure your tap heights to go between the two pipes, Every pipe you will pass will give you a score of one point.

## Organization of Files and Folders

![image](https://github.com/Mnbel555/flappyBird-Report-/assets/125232753/b1db1cdd-c22e-41c1-bef5-e565764bf5d2)

In this  project  there  are  several  folders like  content, projectcode, properties, utilities etc.
`Content`  Content folder are  the  assets  that the  Monogame  framework recognizes  to locate and load images, audios and other files that are not directly part of the game code.
`ProjectCode` this includes whole code for game like character,obstacles,ground etc
`Properties` this contains assemblyInfo of game,it is general information about the application which includes title,copyright, discription, trademark etc.
`Utilities`It contains collections of functions, addition of directories and moving, copying of  files to and from directories

##  Analysis of Code
In this part, code blocks are described like addition of sprites, sounds, scores,controls of game etc.

 <details>
    <summary>Audio Initialization</summary>

```csharp
component.GetAudioSourceComponent().AddSound(@"FlappyBird\sfx_die");
 component.GetAudioSourceComponent().AddSound(@"FlappyBird\sfx_hit");
 component.GetAudioSourceComponent().AddSound(@"FlappyBird\sfx_point");
 component.GetAudioSourceComponent().AddSound(@"FlappyBird\sfx_swooshing");
   component.GetAudioSourceComponent().AddSound(@"FlappyBird\sfx_wing");
    component.GetAudioSourceComponent().SetVolume(0.1f);

```
</details>
<details>
    <summary>Keyboard control</summary>
  
  
  It will check condition if it returns true, it will flap otherwise in case of false it wont work and bird falls down.

```csharp
if (SEKeyboardManager.CheckKeyDown(Keys.Space))
                {
                    Jump();
                }

```
</details>
<details>
    <summary>Changing of sprites</summary>

```csharp
changeSpriteAnim.AddSprite(SEResourcesManager.GetSpriteByName("yellowbird-midflap"));
            changeSpriteAnim.AddSprite(SEResourcesManager.GetSpriteByName("yellowbird-upflap"));
            changeSpriteAnim.AddSprite(SEResourcesManager.GetSpriteByName("yellowbird-downflap")); 

```
</details>
<details>
    <summary>Scores</summary>
  
  it checks whether the condition is true or not and add points respectively

```csharp
 if ((childs[i].GetChilds()[0].GetComponent().GetTransformComponent().GetPositionX() < bird.GetComponent().GetTransformComponent().GetPositionX()) && (childs[i] as Obstacle).IsActive())
                {
                    bird.GetComponent().GetAudioSourceComponent().Play(@"FlappyBird\sfx_point");
                    FlappyBirdProperties.IncreaseScore();
}
```
                                                                                                                                                  
 whereas this checks points and sets new value for highscore  
                                                                                                                                                  
```csharp
 if (SerializationSystem.GetValue<int>("highScore.json") < score)
            {
                SerializationSystem.SaveValue(score);
                highScore = score;
            }
```                                                                                                                                         
</details>
  
<details>
  <summary>Collision</summary>
  this functions checks action of collision and terminates the game

```csharp
 public void Collapse()
        {
            FlappyBirdProperties.SetBirdFlyStatus(false);
            FlappyBirdProperties.GetTextLabel().GetComponent().GetFontComponent().SetText("Tap on space to reload game");
            FlappyBirdProperties.GetTextLabel().SetEnable(true);
            component.GetTransformComponent().SetSpeed(8);
}

```
                                                                                                                                                  
here it wil check condition if bird hits the ground then game terminates 
                                                                                                                                                  
```csharp
if ((GetComponent().GetTransformComponent().GetPositionY() > FlappyBirdProperties.GetGroundHeigth()) ||
                (GetComponent().GetTransformComponent().GetPositionY() < 0))
            {
                component.GetAudioSourceComponent().Play(@"FlappyBird\sfx_die");
                Collapse();
            }

```                                                                                                                                         
</details>

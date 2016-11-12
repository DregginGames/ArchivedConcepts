# Dragon2D/Dragon2DProject build in RT RPG fighting and leveling system

## Huh?
Yes, Dragon2D is gonna have realtile fights with the enemys. I dont like round-based fights. Really. 
(ok pokemon is ok but thats it. i like pokemon).

## Basics
Every Player has 3 Properties that can be cangend every time the player levels up
	* Strenght: How hard can you hit your enemy? Increses HP, ST, DP and AP
	* Intelligence: Think of it! Inceses EN and CN
	* Resilience: You were to fast for that to hit you! Inceses DP and also HP(not as much as Strength) and how fast attacks are dealt
	
Every Character has some basical Resources:
	* Healthpoints (HP): if this reaches 0, the character dies
	* Stamina (ST): if this is 0, you cant attack with Weapons such as swords and you cant run fast. 
	* Energy (EN): this is the Mana in the RPG world of the Dragon2D-Project. Specific actions require a specific amount of EN.
	
Every action the player does besides walking and talking (i.E. fighting, climbing, ... whatever you do) will have an effect on these.
For fighting/energy usage/defense there are also these 3 things
	* Defense Points (DP): Reduces the effects of damage done by enemys. 
	* Attack Points (AP): Increses the default physical attack strength
	* Concentration (CN): A more concentrated player will use energy more efficently ("cast better spells")

And then there are Experience Points, XP, wich are gained by battles, quests, ...
And look, suddenly there is leveling.

## Leveling
Players start at level one with 3 points on every base property (strenght, Resilience and intelligence)
In case of the player he/she can now assign 5 addidtional points to those.
On every levelup, the basic resrouces are refilled and the character gets skill points that can be spend on the base props.

We base our leveling on the following formula:
	SUM(n=2 to levelToReach) of 100*1.3^n
	
	PeateTheSlayer has 120XP, being on level 1. Afer killing the SuperDuperEvilCaveSpiderRiderMonsterDemon he gets 100XP - now he has 220.
	Thats why he levels up to level 2, still having his 220 xp. Now he needs 388XP floor(169+100*1.3^3) to reach the next level.
	If he reches 388XP this value is increased again, 460+100*1.3^4 to 674.something. 
	
## Calculation of the baselevels(if not depleted in case of HP, ST and EN) of HP, ST, EN, DP, AP and CN

	* HP = 20 + 10*Strength + 5*Resilience + 3*level + itemEffects + effects
	* ST = 30 + 10*Strength + 3*Level + itemEffects + effects
	* EN = 20 + 10*Intelligence + 4*level
	* DP = 15 + 4*Strength + 10*Resilience + 2*level + itemEffects + effects
	* AP = 15 + 10*Strength + 4*Resilience + 2*level + itemEffects + effects
	* CN = 20 + 10*Intelligence + CURRENT EN + 4*level + itemEffects + effects

## Attacks and Defenses

If a player attacks, the base damage equals the AP of the player OR the damage of a specific energy effect
	BD = AP or energy effect
	This base damage is incresed/decreased based on the level difference between the oponents, from the perspective of the cause of the damage
	AD = BD (for now)
	Then the random does its thing - the recieved damage is calculated as 
	RD = rand(AD/2,AD)
	finally, the defenses take action, resulting in the actual caused damage
	CD = RD - rand(0,DP)
	
	Attacks on specific attributes (reduces Energy, ...) are not influcenced by any values and cause direct damage.
	
	
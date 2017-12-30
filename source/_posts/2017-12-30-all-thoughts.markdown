---
layout: post
title: "All thoughts"
date: 2017-12-30 04:34:45 +0530
comments: true
published: false
categories:
---

1. Abhi toh ye shuruat hai
Never say 'This is it' or 'this was exactly what I wanted to achieve'
Always say 'ye toh bas shuruat hai'

2. Rails is beautiful
-> Ever wondered why controllers are always named in plural form?
- because of indexes in the routes
- singleton controllers also exist, no big deal. but a lot of thinking has gone into making of rails

    3. Life is nothing but a trade-off between long-term and short-term
- every decision you make will affect you in the long-term. But you just can't keep on thinking about the long-term, else you'll go mad. Sometimes short-term soch k kaam chalana padta hai

    4. The only purpose you have in life is to get screwed

    6. Importance of Test Cases in TDD

- When you are traveling to some place in a car, you usually are playing games on your cell, your sister is watching songs and mother in the front seat is looking out the window. But the driver's full attention is on the road. One thing is made sure that the driver's focus never shifts or an accident can occur. Such is the case in Test Driven Development. Your tests must be full proof in order for your software to work properly.
- - At my intern, I wrote a REST api in RoR for a small project. I followed DRY, Convention over Configuration andTDD philosophy. According to convention, RoR REST api follows a Model-View-Controller structure. You can view the entire project on this link: https://github.com/wallydrag/simple_rest_api/.
 - This api implements the POST, GET, PUT and DELETE methods to maintain a db consisting of 2 attributes: `name` and `age`. The tech stack is Ruby, Rails and sqlite.
 - Take a look at the test for PUT method of the api:
 - RSpec.describe UserController, type: :controller do
     let(:age) {12}
     let(:name) { 'qwerty' }
     let(:age_1) {24}
     let(:name_1) { 'ytrewq' }
     describe "#edit" do
     it "stores under db if resource_id does not exist" do
     put :edit, { age: age, name: name, id: nil }
     expect(response).to have_http_status(:created)
     expect(User.all.count).to eq(1)
     end
     it "updates under db if resource_id exists" do
     args = { age: age, name: name }
     user = User.create_user(args)
     put :edit, { age: age_1, name: name_1, id: user.id }
     expect(response).to have_http_status(:ok)
     expect(JSON.parse(response.body)).to eq({ "age" => age_1, "name" => name_1 })
     end
     end
     end
     Now take a look at the function for PUT method of the api:
     def edit
     if params[:id] == nil
     return self.create
     else
     args = params.permit(:age, :name, :id)
     user = User.edit_user(args)
     render json: { :age => user.age,
     :name => user.name}
     end
     When I run `rake spec`, this test passes without any problems.
     I run these commands sequentially and see what happens:
     A. curl -X POST --form age=12 --form name='qwerty' http://localhost:3000/user/create
     -> Returns id=1 and success.
     B.  curl -X PUT --form id=1 age=21 --form name='ytrewq' http://localhost:3000/user/edit
     -> Returns id=1 and success.
     C.  curl -X GET --form id=1 http://localhost:3000/user/show
     -> Returns age=12 and name='qwerty'

```
     The culprit is lying in the model:
     class User < ActiveRecord::Base
     def self.edit_user(args)
     user = User.find(args[:id])
     user.age = args[:age]
     user.name = args[:name]
user.save
user
end
end
```

7. Correct way to sell

- You shouldnt tell people about your amazing features. People using your product should tell you about those.
- Take example of Apple. After releasing Iphone 7, they are busy telling people what is new and what is awesome. There is a very high chance that people will psychologically be driven to believing some feature is awesome because they say so in their marketing. But to truly test a product by fire, you should just release it to the people. Then they will tell you which features you need to keep for the next time and which features to remove.

8. Intent is fucking everything.
Today, on Oct 7, Debashish stripped us naked. He sat us down, walked us line through line of jenkins jobs and cookbooks. We were through in 1 hours and 30 minutes. At the end, he asked us if we can do it in 90 minutes, what were we waiting for when he had asked us to do it last thursday? Agar intent hota toh humne kar liya hota ab tak.

9. A feeling is very important
- I read a blog about ansible vs puppet vs chef vs salt. Still I didn't remember it. So I was not having a feeling to do it. I just did it for the sake of doing it.

10. Quality curiosity OR Quriosity:
-> Why are CSS scripts so difficult to maintain?
-> Why 75% build pe run ho jaata hai?
-> gradle run pe chalaa aur jetty kyu nahi?
-> In REST api, whose responsibility is it to maintain

11. Honour vs courage.
The blind side beautiful poem.

12. "My prediction that bullet train will cost more than flights!"

13. Be subtle or Be Stupid.

Being subtle is a huge advantage in itself. You save yourself a lot of trouble explaining stuff. Also, your friends will get filtered when you are subtle in your daily life. You will figure out who are the smart folks and who are not the ones you want to be with.
I believe being subtle is so important because of how TVF depicts it in their show. The best example I can give is in Pitchers S01E01, where the conversation takes place in such a way:
Naveen: Bhaiya jaldi chalaao na!
Driver: Itna traffic hai aage, mai kya kar sakta hu.
Driver: Par ek doosra raasta hai Chandimal se. Waha se le lu?
Naveen: Par udhar bhi traffic hua toh?
Driver: Wo toh raasta lenge tabhi pata chalega. Par aap is raaste pe rahoge toh aapki flight pakka choot jaayegi!
Naveen finally decides to take entreprenuership as an option.

14. Who is responsible for women wearing short clothes?
The reason for this post isn’t because I don’t want women wearing short clothes. It is because I don’t want them to wear short clothes out of not wanting to wear short clothes but having to wear short clothes.
- Can it be men? Becoz they gave special attention to those women who are wearing short and seductive clothes? This led women to believe that they will seem more attractive if they wear shorter clothes.
- Could it be women? If one woman started wearing it, others should have stayed true to their self and ignore her. Slowly but steadily us ek ladki ki akkal thikaane aa jati and she would stop wearing short clothes.
Every time you see some girl wearing short clothes and pay attention to her, ask urself this question: Do u really want your mother/sister/daughter/wife to wear short clothes out of helplessness?

15. I have seen people use the word NEVER. It is the most bullshit word in the history of mankind. Never say never. You should never tell anyone you will never face this problem. You should never tell anyone that they can never achieve this feat. Just don't use the word never. Because in my life I have seen complete idiots doing stuff that people had told them they would never be able to achieve those things. So to yourself also, NEVER say NEVER. Probability is a better word. You can say the probability for this to occur is less.

16. thing I learned the hard way.

Until your concepts are clear, no matter how creative you are, no matter how good you are in design, you will always stop at one point. Your mind will not be able to think of doing things differently if you don't know: 1 the basics and 2 don't have the experience.
-> I felt like shouting loudly that this is the best I can think about but just then I remembered about one word a senior told me: "Patience..." So here I am writing this blog post 2 days later. I have atleast realized that to think about all the possibilities, I should 1st know all the possibilities, then know what is the meaning of them and then understand when to use what? The last thing can be learned in 2 ways: By practicing for some time, or by reading what others have practised.

18. Right way to stay healthy

I was inspired to write this post when a senior asked me: “After joining a job, how many months will pass until you gain 20 pounds?” So this post explores all options of maintaining health and the behavior of people that forget about health and all of a sudden start looking for these options.
Firstly, I am no pundit here. I have till now experimented 3 ways to stay physically healthy. Here is the analysis of my experiments:
   Gym!! Oh boy do I hate gymming. The reason most people don’t like gymming is simple. There is absolutely no incentive other than the fact that the next time you are in a swimsuit others might be a bit impressed. The second reason gymming is boring is because most exercises you have to do solo. Without a partner, a difficult job is always boring if you ain’t passionate about it. [1] That is the reason there is music playing in the gym or people with earphones in their heads. Also, in my last 5 years of ‘irregular’ gymming, I have never seen people from the age group of 18–35 come regularly to a gym. Gym is more of a short-term plan for them than a long-term goal to build a healthy lifestyle. The people who are regular are mostly 35+ in age. So either they attend gym out of compulsion or because gym is a part of their routine for the past few years.
       Sports! I believe this is the best way to stay healthy, physically as well as mentally. Just find a group of friends, and play with them any sport daily. Football, cricket, TT, whatever be the sport… You will not require music to pass those 30 minutes; instead 60 minutes will sail away refreshing your body as well as mind.
           Time to get practical.[2] Do a simple non-monotonous exercise for 20–25 minutes that sweats you in an appropriate amount. You can choose any activity: Running, Cycling, Swimming. This is what I do to stay healthy. “A jug fills drop by drop” - Buddha. Don’t stress yourselves on the amount of calories you will burn. Remember that if you keep up this routine everyday, within 1 month you will notice a difference in your physical health. Over the course of 1 year, you might not have dropped 20 pounds but you will definitely be a lot more healthier than before. The best thing about this method is that there’s no burden here. At anytime of the day, you can break a sweat. Also, don’t choose machines for this;instead go into your neighbourhood for a jog/ride to get rid of the feeling of monotony.
Read on to know all aspects and factors leading to people neglecting health.
First, the basics. Recollect your school days. In Primary Section, at the sound of the 'Lunch Break' bell, (almost) every student grabbed his/her tiffin and rushed to the playground. Be it cricket by using the trunk of a tree as stumps or Football on a basketball court using tennis ball as a football, everyone liked to play. Come High School, lo and behold! You find only 30% of the students on the ground. So where are the other 70% students? Majority of them are doing 'something' like hanging out by the canteen, completing home assignments sitting in the classroom or taking walks with their group of friends around the campus like senior citizens!
Analysis of these first signs of behavioral change shows one major reason. Students start getting conscious of themselves by the age of 14. A student who is mediocre at sports starts developing this idea when he gets picked last when teams are chosen for any game. Such students start looking for other options around this time, stumble upon 'something' that they are good at, and this new 'something' defines their life for the next few years.
Another major reason for lifting focus off sports- Academics. Be it parents, teachers or tuition instructors, when it comes to handling academics seriously; sports is the culprit. After passing your matriculate or intermediate examinations, these phrases start sounding familiar: "Watch some television to refresh yourselves!" or "Go play video games for sometime, then resume your studies". You never meet a mom (like mine) who is so cool to put away your books even when your annual exams are going on and force you to go out and get some fresh air by playing something.[3]
Fast forward into the future. You are 30! One unexpected day, the elevator of your office is out of order. You are forced to take the stairs. Moment of Truth!! You can't catch your breath, let alone make it swiftly like before. The past 10 years of life flash before your eyes in a split second: Night-outs, Fast food, hangovers, and especially Desk jobs! This is when people look for short-term goals to get healthy quickly and neglect the long-term options.
[1] Boring jobs are the most important if you wish to achieve something.
[2] In a country of 130+ crore people, it is highly unlikely you’d get an open ground everyday for 60 minutes. Even more unlikely is finding a group of friends as enthusiastic as you for a sport.
[3] This is a 2 edged sword. If you perform badly at academics, you feel guilty that you are not serious enough for studies. Hence, cannot comment on that.
Honorary mention: 2nd best way after exercise is eating healthy food. No debate there. I have seen Patels and Shahs living upto 90 years just because they had a very light diet (Just Khichadi) after the age of 50. But yes, even they did an appropriate amount of physical work in their youth.

19. What do you want to become?

A bullshit question. Nobody knows what he/she wants to do for the rest of his life at the age of 25. I have been playing football for the past 12 years and now I realize that this is the sport I want to play for the rest of my life. I tried TT, badminton, cricket, basketball, skating, swimming, gymming, and karate, and now I have settled on football.
Why is not a good word to throw around. There is no rat race. There is only one race: “Survival”. A deer and a lion have different meanings of survival.
In my experience, hard worker wins. Period. If not immediately, eventually.
My dad didn’t think abt anything else, just that his kids should not sleep hungry at night. I believe he wanted to become a good dad. He obviously couldn’t answer the WHY question but sure did win the what battle.
So for now, fuck the why. Focus on becoming so involved that whenever u find something that u truly love, you dnt have to waste any time and get started right on it.

20. The real meaning of Distraction

Probably the most abused word in English dictionary is Distraction. People use that term to explain why they couldn’t achieve the task given to them.
It’s meaning is: “a thing that prevents someone from concentrating on something else.”
But if a relationship, television, sports can be used to illustrate distraction, how are successful people attaining success while indulging in almost all of this?
The real reason is involvement. When you like something, you wish to stay involved in it. You will accomplish the required things no matter what. When you don’t like something and want to run away from something you use these “distractions” as a shield.


21. Success and Hard Work

I tried to convince her that "In the end it doesn't even matter" by telling her that no matter how much hard work you do, in the end it all comes down to luck. But she convinced me otherwise. She convinced me that the hard work we do might not bear results immediately because of bad luck, but eventually hard work always comes into play. If you have worked hard on something you, you will definitely see it coming handy one day of your life. And as it turns out that will be the most important day of your life.

22. Culture of IITJ

So there is a bapu. All 2nd year students are our fathers, 3rd year grandfathers and so on..
When I came to Bglr, Prashant and Sahil literally treated me like their son. I feel home sick a lot and that’s the reason I talk to home 10–15 minutes a day. It felt like that in college and many a times I couldn’t focus on my studies. But it never felt like that over here. Sahil and Prashant used to ask me almost everyday what I learned,, they asked me whether I have eaten. And I felt pretty bad about not giving them money in sharing, but they refused to take a single dime from me. Be it food, taxi, rent. On the other end, they always told me not to take any tension and stay over at their place till whatever time I want to. Man…
After college, I am experiencing first hand this culture of senior-junior interaction and am really amazed at how really helpful seniors have proven to be. Lets hope I can be of the same help to some junior some day.
So many times I talked to my mom and she remarked: “A blood-relative would not have taken care of you the way these people are taking care of you. When you get the chance thank Prashant, Sahil and Shobhit a lot from my side.”

23. Sane or Sick?

Sick or Sane? I have been asked a lot of times why I prefer staying away from fb. Well, if asked casually, I reply casually: "It is to save time." But some have gone really deep and want to know the real reason why I am not on fb. So I thought lets get started:
A. People never show who they really are on public forums. I like quora a lot because of its Anonymity feature.
B. No. of friends is 891. Really? Haven't talked to 90% of them in the past 4 years. Worse, I hate some people on the inside but can't say to their face that I don't want to befriend you on FB when asked directly. I talk only to my parents and smaller brother on a daily basis. I only talk to 3 of my friends from school on a weekly basis. Talk to 15 of my relatives on a monthly basis and try to stay in touch with 15 seniors on a 3-4 month basis. It's not that I have a very busy schedule. But the activities of day-to-day life are just too overwhelming for me to focus on all this other stuff.
C. Losing control. Whatsapp is really a great tool for 1 reason. I have control. In one week, I have a maximum msgs from around 7-8 people whom I properly know. Whereas on FB, I am being tagged here and there. Too many messages per week from people I don't even know just doing it for time pass. When I will start losing control on whatsapp, I will leave it too. Example of losing control on whatsapp is forming a group where people put all sorts of random forwarded msgs. So, its better to stay out of those groups.
- People fight a lot. Man.. do I hate fights. If someone has an opinion, make a counter. Don't just say that you are wrong or give adjectives to that person.
- Only one good faayda. If one long forgotten friend achieves something, you can see it in your news feed. But surprise surprise. You only remember stuff that you care about. Everything else goes to vain. Example: Piyush is married. 5 days later, I don’t even remember the wife’s name. If I meet Piyush after 3 months, I don’t even remember he was married. Same with friends getting admitted or placed. I don’t remember people’s field of education/ job company unless I really want to.
- Either I am sick or I am sane. No point what I am as long as I accept who I am!
- In life it is not important to have many relations, but extremely important to have life in your relations.

24. Reaping the fruits of seeds sown by others

Had Shobhit not started up and joined Microsoft, I would be a sorry ass right now. So, intelligent people should have a startup and instead of staying home comfortably in a job from 9–5, work your ass off in the age of 21–28 so that others might prosper. India’s weakness is not brain drain. It is the laziness of the people to execute the brilliant ideas they have.
When I first went to C42's office, my mom said this: "Yeh Shobhit bahot hi acha ladka lag raha hai." A middle class family has no other ambition but to make a living worth surviving. My mom had but one wish for me. That I get settled as soon as possible. Had Shobhit not started up, my settlement would be delayed by a minimum of 1–2 months. It is because of such people that there is a ray of hope in the eyes of people like me.
It is our duty to learn from them, and startup in the near future.
After completion of internship, regardless of getting/not getting a job, you gotta thank Shobhit for the support he had given you. An entreprenuer who can create jobs is a person worth becoming man!

25. One can’t move ahead leaving others behind

Climate change is the biggest reminder of Sustainable Development. The Common Man is a witness, who is not fooled by what he sees, because he has seen so much and in a way that is what allows him to survive.Remember the saying "One section of the society cannot move forward by leaving others behind"?Well, it was thought of as being impossible that economic sections can have such huge gaps in income, but it is now a reality. Now the world is faced with another major problem : Climate Change. Gone are the times when a country only deals with its own problems leaving the rest of the world to deal with their own. Now, whatever happens in one part of the world will have global consequences.

26. The irony of Leadership and Freedom

This discusses about how leadership may ironically take away your freedom as compared to the public mojo “My life my way!” I have shared my experiences as a football captain and a brief startup founder.
My football
How entreprenuership ironically takes away freedom. Give example of what you faced on becoming a captain. a) u cant take absence when u want. b) u cant give more time to yourself. c) u have to think above yourself and devise a win-win strategy.
Generalise: When you are in charge, ironically you lose a large part of your freedom.
=> My football team consisted of 29 members [1] and startup team had 2 other juniors working with me.
First lets talk history. When I was in freshman year, I was deeply influenced by 2 seniors
(19 Juniors, 4 batchmates ,5 seniors and me!)

27. Function over Fashion

I have never been so passionate about something but cycling.
Today I had to choose between Fashion and Function. So I chose Function as always. I opted for total mud guard instead of the partial mud guard generally available with such cycles.
So is life. In fear of what people looking at you will percieve, you must not compromise on Fashion over Function.

28. Naya Half, Naya Game… Jai mata Di!

An old tradition continues to exist in the football team of IIT Jodhpur. At the beginning of the second half, we form a huddle and say: "Naya Half, Naya game."( Translation: "New half, new game")
As I complete my B.Tech and move into a new era of life, I believe the new half has started for me.

29. A beautiful girl

- Definition of beauty: "To accept yourself. To live life to express yourself and not impress others. To be beautiful means to be yourself. You don’t need to be accepted by others. You need to accept yourself."
- http://blog.ted.com/how-do-teens-think-about-body-image-beauty-and-bullying/
- Today I want to talk about a girl who is beautiful. According to gossip standards, yes she is fat. She is not fair and lovely white. Not a great hairstyle. Definitely not those hot seductive eyes and lips. In short, this girl would never make the cut of 'love at first sight'. There is a kind of tradition to ask boys their infatuations on day one. In our batch it was Anjali/Sonika just based on physical appearance. This was a batch junior to ours. I properly remember no student ever taking her name.
- I was reading the blog above and one girl came to my mind: Mansi Mittal. No insult to others but I have never seen a girl so bold and expressive as this one, especially if you compare the 'physical appearance' to 'being yourself' ratio.
- There is an air of confidence in this woman that has inspired her to become the first secy in our college. She can probably go on to become the first gen secy too.
- Today, many people are just lost in the insecurities of stuff that never matters but is literally only in their minds. I would love for people to take a look at this girl in public and realize how little those things matter.

30. 'Hypocrisy' vs 'thought of others'?
- In our religion I had heard of a fantastic story to teach children about developing habits and how that one habit will become fruitful one day. A beggar met a monk who asked him to keep any one habit daily. He joked saying 'I will not take breakfast without looking at the potter's donkey's tail in the morning. Then one day the potter had left early for digging and the beggar was very hungry. So he went out in search of the donkey's tail. He saw it and the potter had just discovered a hidden treasure from beneath the earth. The beggar exclaimed: 'I saw it. I saw it!"
- I have a contradicting opinion. Habits are only so good as long as you aren't in the way of others. I for example am a Jain. As a rule, we don't bring potatoes, onions, etc. in our home. But when we have guests coming over, we don't enforce this rule on them and bring in potatoes for their taste. The same happens when we go out for functions. We eat non jain food in case there isn't jain food.
- This brings me to a point where I am at a debate with myself. Is it plain hypocrisy to allow flexibility in your rules and define your religion as you feel comfortable. In the future it is entirely possible that I would start eating non-vegetarian food just because I don't want to cause 'inconvenience' to others. Or is it that my religion teaches me to care about every single micro-organism in the world. So the least I can do is spare a thought for others and adjust myself according to the situation.
- In the end, I have settled on one thing. It is definitely hypocrisy if jain food and non-jain food both are available and I decide to eat non-jain food. But in the case of 'inconvenience', I will have to draw a line as to where I would stop in case I am causing inconvenience to others.

31. Rationale without Reason
- My admission into English medium was because of 1 stupid reason: "My dad had a transferable job and if we move out of state, I might not get a Gujarati medium school."
- Getting me into the football team was only because cricket was very costly and they needed me to buy a 1500 rupees kit. Today football has turned out to be a major asset in my life.

32. A journey of a jobless guy to a PRO-grammer
- this is my journey since June 2016. I have learnt one thing after joining this company. Nothing is impossible if you put your mind, heart and hard-work to it.
- - So I will post every tiny little thing that happened with me that people reading should be careful about. Probably not all of my blogs will help you but I can guarantee that atleast 10% of my blogs would make a 90% difference to your life

33. Keep spelling mistakes in mind
- Yesterday, my pair wasted 3-4 hours of his time because of a spelling mistake I made. Gosh, I felt very guilty. He had to stay up till 4 am so that we fixed that and start working on something else today.
- - But he was very patient towards me. That's good because it helps people at lower level to grow.
- - cookbook was active-booking-service. See commit 'spelling mistake' for more context

34. When working with arrays and hashes, indexes matter
- Today approx 2 hours of my life were wasted because I wasn't able keep the indexes in mind.
- This is a part of s/w dev process but I want you to learn from this and not repeat this in your life.

35. Being lazy helps
- Postgres doesn’t consider null values equal for a column with uniqueness constraint. Whereas rails does.
- My partner was hell bent on researching more about this, all I did was undo our changes and we were good to go.

36. Building phone anonymization service for 250,000 drivers and 20,000,000 customers
37. Effort replaces hard work
- One thing I would like to point out is we should stop using the terminology "hard work". Dude what the fuck is hard work? That is just so subjective. We should start using "make an effort". Some will put in more effort, some will put in less effort. But everyone will be happy/satisfied that they are putting in some effort and people's satisfaction is really all that matters.
- - Almost everyone can be overwhelmed with working hard. But no one will be overwhelmed by putting in effort. Best example I can provide you is my phase in 11th std. I studied just 2-3 hours everyday. It wasn’t at all overwhelming. And 2 months down the line I started getting 1st rank. For the first 4 months I didn’t study anything just because I kept on hearing from people that I should very hard. Minimum 10 hours of study per day.


38. Market for affordable and long-lasting phones
Just like cars. Cars like Etios and Verito are bought/trusted by drivers. We should have phones like those in the 200$ range for drivers/courier guys to keep. There is demand for this kind of things

39. Never do select  FROM any_db
When you add a column to any table, and the select  query is mapping it to an object, then...
 if you run migrations first, the code will fail as db starts returning an extra column. If you deploy the code first, then too it will fail as the db is returning one less column. Wow man Niranjan

40. Listen to your teachers
 one day mr. Biju jose started off by telling us an unusual story of his encounter with a traffic police. How he tried to make him understand his situation and escaped the penalty.
 a similar incident happened with me. I was on my way back from my coaching classes and a police officer stopped me and asked for my license. I did not have it. I told him about the condition in my house. We had only one two wheeler so if this one got confiscated we would have a lot of problems. He understood and let me go.

40. Use jump defs a lot.
jump defs help more than googling random stuff. You get to deeper levels into the code, you find out more ways in which things can be written man.

41. When you don’t know what you’re doing, STOP
So here we are, wrote the entire ABS code within 3 days. And I bet you it was working. Guess what we do next. Spend 12 days refactoring/restructuring it.
Stop my dear friend. Ask google, then ask the community, then ask your mentor, if things still aren’t clear, take some time off and study. But be committed to writing good software.

42. You never revisit your code
It is very important that you code to the best of your abilities. If you leave broken windows and leave, you’ll never find yourselves coming back to fix them.

43. The virtue of patience
Services right now are faster than ever. AC cools the room very fast, mail instead of physical letter.
what I am trying to find is does this affect our attitude in any ways?
Are we losing the virtue of patience?

45. Is love between couples decreasing?
The culprit is communication. Because we communicate so much, there is no desperation, no urgency at all.
In the days before this, the couple hadn’t interacted for weeks before meeting. The thoughts of what would be going on, the anxiety of success of your partner in their efforts, everything played a huge role in longing for your loved one.
Now you know almost everything about your significant other because of texting/daily communication. So when you finally meet, there are just no questions to ask each other. You end up spending time in front of the TV, or engaging in other entertainment activities.

46. The correlation between commitment power and alarm habits
What is an alarm after all? It is a commitment you are making to yourself, that  will be fulfilled in the next 6-10 hours. If you are not able to keep that only,,,
Look at our parents for example. They have more commitment power that us because of their alarm habits. They didn’t set off the snooze button like we do.
this is just a probability, and an initial thought

47. A school picnic at the age of 22
No expectations, I tried to organize stuff and make sure everyone has a good time. I wanted to make sure everyone gets to have fun and people return home with a smile on their faces.
What I didn’t know was that it would build up on every single moment.
The best part of my picnic was we won gold medal in football. We were literally the underdogs. Placed at 3rd position statistically by the skill of players, this was the one place I felt strategy overpowered skill
we gave away zero penalties because of fault of defenders, we capitalized on the penalties provided to us by other teams
The defense was absolutely resolute man! Mehak was trying to make attacks single handedly and even scored single handedly!
We had the advantage of a good goalkeeper. I had finally understood that a match result in 5-a-side football depends heavily on the quality of your goalkeeper.

48. Read fizzbuzz page on c2 wiki
The first line reads that fizz buzz test screens 99.5% of the programmers. So it is indeed very important for you to read.
Just go through the approaches taken by different programmers all through history have taken and you’ll understand how important this test really is.


50. I had this idea
There are aspects of the platforms that genuinely do increase drivers’ control over their work lives, as Uber frequently points out. Unlike most workers, an Uber driver can put in a few hours each day between dropping children off at school and picking them up in the afternoon.
Uber is even in the process of developing a feature that allows drivers to tell the app in advance that they need to arrive at a given location at a given time. “If you need to pick up your kids at soccer practice at 6 p.m.,” said Nundu Janakiram, the Uber official in charge of products that improve drivers’ experiences, “it will start to give you trips to take you in the general direction to get to a specific place in time.”

51. Don’t celebrate football goals in the side
it is surprising nobody gave a thought to this, yet. After scoring a goal, you shouldn’t head to the corner and celebrate with your team. I mean, what is the impact of that on hearts of opposition?
you should celebrate right at the penalty spot. let them know that you own their penalty area. Instill fear in the hearts of their goalkeeper.

53. Are open office spaces doing justice to employees?
- I would like you to take a moment and look at this famous picture: equality vs justice
- - My dad is in a conventional company. I hate the place where my father works. I desperately want to get him out of there as fast as I can. The reason? There is jee huzuri over there. Everyone doesn’t sit on the same table. Everyone’s opinions aren’t taken that seriously. So when I told him that the MD of India, CTO, and all VPs sit on the same table as I do, he simply couldn’t believe me that there aren’t cabins for special people. This is the best thing about open office space. It gives the vibe of equality and freedom.
- - android guys need more charts, more ways they can visualize stuff and get quick feedback from surrounding people
- - backend guys do need a lot of whiteboarding. Aishwarya and I were working on a story that would take about 4 days to complete. Because we whiteboarded the problem, asked Shridhar for a little more understanding, we practically brought the work down to 2 days. The first time we did this, we discussed this with Dinesh and Chandra, but were so engrossed on continuing with dev work that we couldn’t really understand what the problem we were trying to solve. So we faced a lot of questions/doubts when we were actually implementing the solution. We stopped, took a step back and whiteboarded about it. Voila!
- - noise is a lot. I would ask you to take a step into the meeting rooms or coder caves at approx 12 PM in the day. or reach office early around 8.30. For 90 minutes you will feel eternal bliss and actually hear the difference between silence which helps you focus and noise which distracts you a lot.

54. Trust your juniors
I reached the chief architect of our company with the implementation of a certain thing. He clearly disagreed on it. He put some points that might make us revert that decision. But in the end, he let us take that decision anyways.

55. Weird naming in golang
you can map cfg to config, ctx to context, but some mappings are very weird
when you name receivers as short form, you are creating an extra overhead in the readers’s mind that cd maps to callerDirectory, etc.
so you are saying that sometimes use longer names, sometimes use shorter names, I am suggesting always use longer name. the 4 things of

56. Don’t use regex to set config values.. Ever
set .*booking-log to consume all topics for this name
then I started publishing to standard-booking-log which had a different schema. Fortunately, it didn’t break anything on production. Just the consumers in integration environment couldn’t parse the message that’s all. Just the consumers in integration environment couldn’t parse the message that’s all. Just the consumers in integration environment couldn’t parse the message that’s all.

57. store http conn deadline in a config
when a client terminates a connection after 100 ms, server should know that if it cannot deliver within 100 ms, prepare to stop utilizing resources.

==> Ideas for a project:
- Radio station with Ad blocker
- - Online school, community like stack overflow with full anonymity
- - Game of Life without using any conditions
-
-  ==> Mind:
-  - Flute learn
-  - Yoga, pranayam
-  - gautam swamy raas
-
-  ==> Body care:
-  - http://www.wikihow.com/Care-for-Your-Teeth
-  - http://www.webmd.com/oral-health/teeth-and-gum-care#1
-  - https://www.mentalhealth.org.uk/a-to-z/p/physical-health-and-mental-health
-  - http://www.wikihow.com/Take-Control-of-Your-Health
-  - http://www.makeuseof.com/tag/four-simple-steps-to-improve-your-sleep-patterns/
-  - http://www.mayoclinic.org/healthy-lifestyle/adult-health/in-depth/sleep/art-20048379
-  - http://www.helpguide.org/articles/sleep/how-to-sleep-better.htm
-  - https://sleepfoundation.org/ask-the-expert/sleep-hygiene
-  - https://www.uhs.umich.edu/tenthings
-  - https://www.mentalhealth.org.uk/publications/how-to-mental-health
-  - http://www.mentalhealthamerica.net/taking-good-care-yourself
-  1. Drink 2 glasses of water before sleeping
-  2. Exfoliate your scalp once a week using an exfoliating scrubber. Also exfoliate your face.
-  3. take a balanced diet of protein, vitamin B
-  4. Moisturise your face, especially the area around the eyes
-  5. Eat walnuts, dates, almonds, kaju and draksh a lot. (Vitamin E)
-  6. get UV protection sunglasses. It is high time you bought those.
-  7. Vitamins C and E, zinc, lutein, zeaxanthin, and omega-3 fatty acids are essential for healthy eyes. Carrots, peas, spinach, oranges
-  - look decent, dress classy, politeness, etiquette, long hair
-  - eye checkup, new and anti-glare spectacles
-
-  ==> Blood donation
-  - Two locations for blood donations:
-  - Manipal hospital
-  - Rotary Club indiranagar
-
-  ==> Diary debt
-  --> http://www.msn.com/en-in/health/fitness/10-stretches-to-keep-you-fit-for-life/ss-BBpEaUq?ocid=wispr
-  -> http://blogs.psychcentral.com/leveraging-adversity/2014/10/want-to-be-mentally-tough-stop-doing-these-five-things/
-  -> http://www.forbes.com/sites/alicegwalton/2015/03/02/growing-resilience-7-strategies-to-become-mentally-stronger/#23481bc75a5e
-  -> http://www.wikihow.com/Be-Mentally-and-Emotionally-Strong
-  -> Face your fear of coding. You'll definitely be able to overcome it.
-  -> Finish things written in memo of phone.
-  I am 25 and very lazy, what should I do?
-  I am going to tell you one simple truth. No matter how many motivational videos you watch or self help books you read, it is not going to help you. Not one bit.
-  For normal people it might work, but for us it will motivate us for an hour hardly and then it all goes away and we are back to square one.
-  I can say this because I was (or am) very lazy and I had tried literally every-freaking-thing there was to get me out of my comfort zone (which was to sit all day long and browse the internet). Trust me, I was one of the laziest asses in the world lying around Quora all day long. My days were as worthless as my nights. In fact, my nights were more productive than my days because I was as productive as most others during those 8 hours. There were many who claimed to be excellent  procrastinators, but I was their king. My inertia was so high, that I spent days together without doing anything constructive. Yet, if this has worked for a sleeping donkey like me then there's a great chance that it will work for you too.
-  There is a very simple solution to do this. First and foremost, it is really important to get some physical activity. You really need to get your ass off from wherever you are sitting or laying right now. I cannot stress this point enough. From your description it seems to me that you tried to go to the gym and it didn't work out. That's probably because you yourself don't enjoy going to the gym but you did it anyway because many others do. Don't do that now, you'll not be able to do that. Normal people might consider this as bad advice but I know how it feels to be super lazy, I've been there. Instead try to do some other form of exercise you enjoy, like jogging or sports or swimming or something else. Literally anything. Find your most enjoyable (or least objectionable) physical activity and do it. Do it everyday. Do it enough to make you physically exhausted. Your mind cannot perform well if your body is loafing around the house watching cuddly cat videos day in and day out.
-
-  Once you start doing something regularly other than browsing the web, both your body and mind will start to loosen up a bit. You will feel more energetic and this will decrease your laziness quotient by some factor. Once your mindset has improved a tad bit, find a few things you enjoy doing or are good at and try to excel at them. If you truly find something you enjoy doing, your mind will automatically take away the rest of the noise. You will gradually stop over thinking about what to do and start doing things.  Don't think about what you have to do, just do it. Nike has done it, you too can. Don't do it because you have to do it. Do it because you relish it and see to it that it is not an utter waste of your time.
-
-  Another very crucial factor is focus. For us lazy-tards, getting our minds to work at full focus is similar to reaching atop a big mountain. It's very difficult to get to that point, but once you get there, it's relatively easy to stay there. Most of your effort should be on getting into the zone. The easiest way to get your mind to focus at a particular thing is by not thinking about absolutely anything. Just give all your attention to one particular thing at a time and forget the rest. Forget that this world exists, or that you have a favourite TV show in 2 hours. Your phone should not be in your room. Your mind should be a clean slate before you start work. Then put your maximum effort to get into the zone because that's where our biggest hurdle lies. Once you are fully into the zone, you will be surprised to see how easy it is to keep on working for hours together. Our minds are surprisingly obedient if you know how to treat them. You can do some non-distracting activities like drinking water or going to the loo. But don't login to Facebook or Quora. If your brain gets even a sniff of any incident or a fun fact, you will quickly lose your focus.
-
-  These things should get you off your feet. Once the wheel starts rotating you will not find it difficult to pick up speed. I still get into lazy mode at times, but I know how to get out of it now. Remember, we are not truly lazy, we just have high inertia. Once you start doing things, then it's not that difficult.
-
-  Life:: baadme ye sab karna.
-  -> Before eating 3 navkar.
-  ~~> Schedule (It is dertermination. woh ayega toh subah bhi tu uth payega. following this will increase confidence)
-  -> Pranayam between 6 and 7 pm.
-  -> Remember self-awareness is the key.
-  -> Go talk to Khokhar everyday. He is like you after all.
-  -> Read kindle when you feel like watching a video. Also, incorporate things read in kindle in life.
-  -> Future: Pick only one thing and not time wise. Complete that one thing, then move on to next thing.
-  -> Dhoni: I  am somebody who has always believed in the present. So you wont get answers regarding the future that is too far ahead. Learn from this and start preparing for the present before making too many plans for the future.
-  -> What are the top 5 hobbies that make you smarter?
-  1. Reading and Writing:
-  I read everyday. It varies from 30 minutes to 3 hours. And I feel I have become way lot smarter (at least I like to think this way).
-  Currently, I am reading 2 books, "Topgun On Wall Street" and "Made In America - Walmart Story".
-  I buy more books than I can actually finish. it has always been this way.
-
-  I make sure that I write everyday. I write a blog: Life is our oyster
-
-  I write about Music Theory, Life, Wisdom, Computer Science, Mathematics, Humor, My Travel experiences, Anything and everything that life is making me experience. Nothing too fancy, but it will make you think.
-
-
-  2. Online courses:
-  Currently, I am doing Machine Learning and Linear Algebra. More than anything, courses for self learning enables you to see the bigger picture of subject.
-  I register for more courses than I can actually complete.
-
-  3. Exercise:
-  There is much more to fitness than getting that 16 inches bicep or 6 packs.
-  Fitness isn't for shape. It's a lifestyle that I follow everyday.
-
-  Eating right is also crucial in being fit. I eat completely healthy food for 6 days in a week and Sunday is always a cheating day for me.
-
-  I workout for 5 days in a week. No excuses.
-  I work on Calisthenics, Cardio respiratory fitness, Circuit training, Drop exercises, Core, Cross training.
-  And this feeling of being fit is something that gives me immense confidence throughout my day.
-
-  4. Music:
-  I have been into music for past 16 years. And I am 23 years old. I try to practice almost everyday. I believe that listening to technical music (read Advaita, Agnee, Muse) is the most important part of mental training of a musician.
-
-  I am an independent musician and a part of various music projects. I play Tabla, Drums, Cajón, Conga, Djembe.
-  I have had formal training at Rockschool.
-
-  You guessed it right. That's me.
-
-  In 2012, I had the privilege to play on percussion with the world class musician Tal Kravitz at Rendezvous 2012, IIT Delhi.
-
-  5. Sports:
-  I play everyday.
-  Learn how to learn.
-  Learn how to live.
-  Learn how to grow.
-  Learn how to improve everyday by 0.01%.
-
-  Go bears. Let's make history.
-  -> The video of Ted Why it pays to work hard is awesome. If you are a C student and not an A student, work hard and it will pay off. Many smart people don't achieve much success coz they rest on their smarts.
-  Funda:
-  a. talk to people only when needed or talked to. Poora introvert banne ki koshish kar.
-  b. No videos, just kindle and g4g!
-  c. Try to study as much as you can in daylight.
-  ~~> Point system:
-  1: avoided talking with group in order to study. Not such a big achievement but definitely big for me.
-  ~~> Don't break these rules.(Don't make a law that is ignorant of the past and insensitive to the present.)
-  -> Don't write a rule unless you are sure you can follow it.
-  -> -> Get more sunlight. try to go to terrace at 6 pm.
-  -> Coconut oil is best.
-  -> Drink a lot of water.
-  -> Eat more walnuts (Akhrot) Copper is also found in blackberries, pineapple, pomegranates, almonds and pumpkin seeds
-  -> Good sleeping habits will help you relax, fully rejuvenate and reduce stress levels.
-  -> Eat foods rich in B12 like eggs, cheese, bananas.
-  -> Circulation and blood flow is vital. . There's no point eating all the vitamins and minerals if they can't reach your scalp and hair. To improve circulation exercise regularly. Also massage your scalp with your fingertips daily for 5-10 minutes to improve circulation.
-  -> go get some baadam. soak in water overnight.
-  -> Count 3 navkaar before eating anything!
-  -> Important to bring some discipline in life! Look at Israel and Japan for example. They have attained great heights only because their citizens were disciplined.
-  -> Inner peace is important to succeed in life. When water in pond is still, no matter how deep the pond is, you'll be able to see things clearly inside it. But if you throw a stone in the pond, it will create ripples. As the stillness of the pond is disturbed, you will unable to see anything inside the pond. Similarly our inner treasures come out only when we have a peaceful mind.
-  -> Visualization
-  I look at myself in the mirror each morning and visualize myself as a confident, successful, attractive, and valuable/helpful individual.
-  I go over key traits mentally each day, the traits that I wish to improve upon the most.
-  I've tried and tested this trick several times in different form before basketball games as well, and it seems to be quite effective. (I visualize for 15 minutes going through each drill in my head, going over the proper balance, form, and techniques. Shooting, rebounding, passing, ect.. I go over everything.) It definitely seems to have a noticeable impact.
-  Cold Shower
-  Starting the day with a cold shower not only gives you a nice boost of energy, It's a great way to face one uncomfortable situation before the day even starts, and it influences the rest of the day.
-  Making Your Bed
-  This one is so simple you might think it's stupid, but making your bed first thing in the morning gives you a feeling of accomplishment. It sets the tone for the day.
-  Meditation
-  I meditate every night before going to bed. I do it to ease mental and/or physical tension, and to get into the right state of mind before falling asleep. Every time I do this I wake up the next morning feeling calm and at peace. The entire day is better because of it.
-  There you have it. Four simple psychological tricks that you can easily follow and develop into daily habits.
-  ->As you study this book, and continue with programming, remember that anything worth doing is difficult at first. Maybe you are the kind of person who is afraid of failure so you give up at the first sign of difficulty. Maybe you never learned self-discipline so you can't do anything that's "boring." Maybe you were told that you are "gifted" so you never attempt anything that might make you seem stupid or not a prodigy. Maybe you are competitive and unfairly compare yourself to someone like me who's been programming for more than 20 years.
-  -> Whatever your reason for wanting to quit, keep at it. Force yourself. If you run into a Study Drill you can't do, or a lesson you just do not understand, then skip it and come back to it later. Just keep going because with programming there's this very odd thing that happens. At first, you will not understand anything. It'll be weird, just like with learning any human language. You will struggle with words, and not know what symbols are what, and it'll all be very confusing. Then one day BANG your brain will snap and you will suddenly "get it." If you keep doing the exercises and keep trying to understand them, you will get it. You might not be a master coder, but you will at least understand how programming works.
-  -> If you don't get a job, don't be disheartened. Analyze what you don't understand and work hard on improving it.
-  -> keep a pack of parle g in your bag at all times.
-  ->data structures learn karna zaroori hai chandu.. bhai aankh mathi aansu nikadi rahya che k bhanyo nathi hu kai...
-  -> 1. Made use of phonetics and detected a 1st year student was from Gujarat just after he said the word: "Na". In hindi, "Na" ends with "AA" but in gujarati, "Na" ends with "Aan".
-  2. Pressure is very good. If there is no pressure or competence, you will never give the best result. Sarthak and Aenik did not get into IIT. So there was no pressure on me to work or study hard. Jo result ayega woh chalega aisa bol k rakha tha. But agar pressure daal k rakha hota toh phir I guess me better perform kar pata.
-  3. A website where every entreprenuer writes all about his/her past. So that people can read. There should be even embarassing content. Show people how entrepreneurs overcame the embarassment thing and started up.
-  4. My super hero has got to be Spider-Man. I like the superpower of releasing a web from your wrists so that you can grab anything. Like after I have taken my seat and suddenly I see my water bottle, I just want to do what Peter Parkers used to do when he wanted things.
-  5. A friend is needed who will stand up for me. Like the moment in 11th std when I was humiliated for being bold and speaking my mind to him. It was his fault too, but because he had a group of 5 people, he was able to silence me into thinking that it was entirely my fault.
-
-  ~~> Jobs:
-  -> Make photo of god. Inclusion: Parents, chote, football, friends, bothra, now I really feel I should leave thinking jainism as my religion..god is someone who shapes your life or helps you shape it.
-  -> Make a video of 5-10 minutes for your motivation. Include every quote, video, pic which motivates you to 1st change yourself and as a result, change the world. 23.00 to 27.00 vishy anand video. cant do 1 percent of what u think u can do.
-  ~~> TuDu:
-  -> Watch movie "The man who knew infinity"
-  -> Two things to learn from today's match 1. Don't give up till the end 2. Don't celebrate before you win! #IndvsBan
-  -> Shut off this family problem business once and for all.
-  -> the power of habit. read this book
-  -> dont look at a day as agar achi shuruaat nai hui hai to phir poora din bigad gaya. look at it like agar achi shuruat nai hui hai to ending toh dhamakedaar honi chaiye
-  -> look at everything like a way of life. exercise, entreprenuership, studying, hard work everything is a way of life.
-  -> http://www.msn.com/en-in/health/fitness/35-everyday-ways-to-keep-your-mind-healthy/ss-AAfyvHE?ocid=wispr#image=2
-  -> I cherish this quote from the Kingsman: The Secret Service movie - (originally by Ernest Hemingway) "There is nothing noble in being superior to your fellow man; true nobility is being superior to your former self."
-  -> lets go to Bhutan one day. It is a beautiful country. You will never feel like coming back.
-  -> http://www.msn.com/en-in/entertainment/bollywood/14-underrated-bollywood-movies-you-must-watch/ar-BBolfMd?li=AAggbRN&ocid=wispr
-
-  -> http://www.msn.com/en-in/health/nutrition/the-best-foods-to-eat-every-day-to-lower-your-blood-pressure/ar-BBpB2VM?li=AAggbRN&ocid=wispr
-  -> http://www.msn.com/en-in/health/medical/5-tips-to-avoid-cancer-from-a-doc-whos-devoted-his-life-to-preventing-the-disease/ar-AAeOkFw?li=AAggbRN&ocid=wispr

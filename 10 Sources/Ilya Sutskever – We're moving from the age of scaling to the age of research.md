tags::
source:: https://www.youtube.com/watch?v=aR20FWCCjAs&list=WL&index=5
type:: #source/article

**From 2020 until now we have been in the age of scaling**
- With the release of ChatGPT companies realized that scaling could lead to repeatable improvement
- However, research, tinkering is not guaranteed
**From no onward we are moving back to the age of research**
- No that the models 
- We have trained all these models on all the data in the world. Pre-training data is what makes these models today. Behind each model we have the same things because they are all trained on the same data anyway. To find novel solutions to AI we need to discover new methods 

**Emotions as [[value function]]s**
There was a study on a boy who had a stroke and lost his ability to feel emotions, this disrupted his ability to make decisions such as what socks to wear and lead to him making some poor financial decisions- [[Somatic Marker Hypothesis]]
- this says something about how emotions function as value functions for us to decide what is the best decision to make
- emotions are highly effective in how they can guide humans to make them learn
- emotions are a way for to make very quick decisions based. Making decisions is the basis for learning. [[It is not the people who make the best decisions that are the most successful it the ones to make the most decisions and continuously iterate on those decisions.]]

**What are some new approaches to build AGI?**
[[Continual learning]] as an definition for [[AGI]]
	A deployed learner that improves on the job is functionally super intelligent
	==Humans generalize better and learn with far fewer samples due to evolution and build-in [[value function]]s.==
Suppose we have two humans who want to be the best competitive programmer in the world
	programmer one, put's in 10,000 hours memorizes all the patterns and wins first place
	programmer two spends 1000 understanding these patterns makes it to second place
In life the second programmer is better because it is able generalize with fewer samples and has better built-in [[value function]]s


**How is [[reinforcement learning]] done naively**
- You have a neural net and give a problem to solve
- The modal has 1000s of actions to produce a solution
- You use a score to provider a training signal for every action in the trajectory
- **If you are training something that goes for a long time the agent will not do any learning until the problem is solved**
	- In the [[Deep Seek R1]], the space of trajectories is so wide that is makes it difficult to learn a mapping from an intermediate trajectory and value.


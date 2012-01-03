# OUTLINE

<es>I like the concept of layers, the Macro -> Micro as you did it is the right thing. 
Same goes to "Going faster", so it seems like we have four main chapters, each with five sub chapters. Seems right, we should keep them short and sweet.</es>

* Introduction
* Layers of Learning
	* Culture (don't waste)<es>What do you mean by don't waste ? </es>
	* Test-Driven Development (how should the code behave?)
	* Continuous Integration (how new code affects existing code)
	* Immune System (how external behavior and internal deployments change actionable metrics)
	* Continuous Deployment (how to resiliently introduce change)
* Going Faster
	* Year    -> Quarter
	* Quarter -> Month
	* Month   -> Week
	* Week    -> Day
	* Day     -> Hour

Case studies and techniques to be mixed into appropriate time periods.

# TECHNIQUES

* Minimize IO in tests tests
* Building domain data setup for testing using factories, easy to evolve tests
* Discovery system + client side routing (no vip)
* Infrastructure as code (devops ftw, gives devs freedom and responsibility over execution env)
* Validated learning (Eric Ries)
	* ideas -> Build -> product -> Measure -> data -> Learn -> ideas -> ...
	* Minimize time throught the whole loop
	* Every problem only once
	* Stop the line if anything fails
	* Fast response vs. prevention

# CASE STUDIES

* David Fortunado (Wealthhfront): Deployment Manager
* John Allspaw (Etsy)
* Eric Ries/Brett Durrett (IMVU)

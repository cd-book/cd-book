# Adam Rosien (Box) #

http://www.slideshare.net/arosien

* Development
	* Trunk-stable
	* Small commits
	* Trivial rollbacks
	* Broken build: no checkins
	* Data migrations: only add fields/columns; only delete when you can prove there are no more consumers of old format
* Test
	* Only automated testing
	* Forbidden calls
		// Use version with explicit math context
		"java.math.BigDecimal#divide(java.math.BigDecimal)",
		"java.math.BigDecimal#setScale(int)"
	* Bad code snippets
	* Injection test: test your dependency injection system
	* Visibility test: packages, methods, fields
	* Stuff-not-tested-test
	* Package dependency test
	* Pre-commit test suite
		* Because our continuous integration system can run our entire test suite much faster than a typical engineer's development machine, we often check in code without running all the tests on our local box. Boo! As you might expect, this leads to more build breakages. However, more often than not the tests associated with the particular checkin would pass (we do have standards after all) but our "meta-tests" would fail due to a bad code snippet, or unintended package dependency violation, etc. This much smaller set of tests is the most common form of a broken build. To lower the chances of a broken build we create a test suite that engineers can quickly run before each commit that contains the most frequently breaking tests in our system.  Each developer can customize this so that they can add tests or suites that they themselves often break or feel extra responsible for (to counter their full-test laziness).
	* Disallow IO in tests
	* Commit-triggered review
		* We don't have time to review every checkin to the codebase. We've broken things most often when dealing with database schema updates and associated data compatibility issues. There are critical times like these when more than one pair of eyes should look things over.	Installing some fancy review or "workflow" system can be both expensive and disruptive, and, well, pointless. You should trust your developers, and enable them to increase their trust in each other. The simplest thing that could possibly work is to have reviewers get an email. For operations-related commits (database-schema-related changes, etc.) just add a #review tag to your commit and everyone on the ops list gets an email with the details. Or add #cc:<username> and those users will get an email too.	Our Deployment Manager (see below) watches the SVN commit log and sends the email when the right hashtag is recognized.
* Continuous Integration
	* Commit message can trigger actions: #deploy:um #pleasereview #cc:ben
	* Test Suite Randomization
		* We had a strange situation where the build would non-deterministically fail, but only very rarely and only on some boxes. We finally figured out that it depended on which test ran first, a classic case of the state of one test leaking into another. Also note that most test suite runners create a predictable test order which works against you in situations like these.	In order to increase the odds of detecting non-deterministic test failures from leaked test state, we both, for each build, randomly divide our tests into isolated groups and randomly order the tests within each group.	JUnit TestSuite generator from a classpath.
	* Disallow Checkins If the Build is Broken
* Branch in code
	* Experiment tags per user
* Continuous Deployment FSM
	* Accepting traffic -> Unannounce -> Clients stop requesting -> Shut down -> Start new version -> Self-test -> Announce -> Accept prod traffic -> Automated rollback
* Deployment
	* Deployment Manager
	* Commit-triggered deployments
		* Why have to go to a web page and click a button to deploy? If you already trust your builds, and you know when you're committing that you want to push that code out, then just deploy automatically if and only if the build passes.	Tag your commit with #release:<service_type> and the Deployment Manager will deploy that service if the build with that commit passes.	DM polls Hudson API for commit messages and build state.
	* Service self-test
* Production Immune System
	* Exception Bus
		* All exceptions are logged and emitted to the Exception Bus. Service "owners" are notified from a lookup, and bugged every N hours if they don't acknowledge the exception and then mark it as "fixed" or "ignore".	RabbitMQ for messaging. Esper for aggregation and thresholding.
	* Long-running queries check: http://eng.wealthfront.com/2010/11/monitoring-long-running-mysql-queries.html
	* Unsigned Report Report: for business-centric reports

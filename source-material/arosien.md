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
	* Bad code snippets
	* Stuff-not-tested-test
	* Disallow IO in tests
* Continuous Integration
	* Commit message can trigger actions: #deploy:um #pleasereview #cc:ben
* Branch in code
	* Experiment tags per user
* Continuous Deployment FSM
	* Accepting traffic -> Unannounce -> Clients stop requesting -> Shut down -> Start new version -> Self-test -> Announce -> Accept prod traffic -> Automated rollback

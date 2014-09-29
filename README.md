solr-drupal
===========
	Requirements:
	(To be installed with aptitude install…)
	• openjdk-7-jdk (Requires Debian 7)
	• Daemon
	
	General Installation
	1. Download Apache Solr with Drupal config here:
	https://github.com/sgurlt/solr-drupal
	(Use the Button "Download Zip" in the bottom right corner)
	2. Copy it to /etc/solr/ (create the folder "solr if it does not exist" on your server, now your folders should look like this /etc/solr/solr-4.9.0
	3. Configure your access file:
	/etc/solr/solr-4.9.0/mysolr/etc/realm.properties
	
	Example:
	admin: drupal,core1-role
	(user: pw,group)
	
	Additional information:
	http://muddyazian.blogspot.de/2013/11/how-to-require-password-authentication.html

	Setup Solr as a service
	1. Move the service file to your /etc/init.d directory
	mv /etc/solr/solr-4.9.0/mysolr/solr/solr /etc/init.d/
	2. Make sure that the file got the permission 755
	chmod 0755 /etc/init.d/solr
	3. Add the Service
	update-rc.d solr defaults
	4. Now you are able to control your service with the following commands and it will automaticaly run on server startup.
	Service solr start|status|stop|restart
	
	Additional information:
	http://stackoverflow.com/questions/2150767/how-to-start-solr-automatically
	
	Setup a new collection
	1. Solr by default is running on Port 8983
	2. The Solr webinterface can be reached using the address: <IP>:8983/solr
	3. To login use the data you added to your realm.properties file
	4. On the server, you've to copy the folder 'collection_drupal_default', it contains any configuration drupal requires to work with solr.
	cp /etc/solr/solr-4.9.0/mysolr/solr/collection_drupal_default /etc/solr/solr-4.9.0/mysolr/solr/<your_new_collection>
	5. On the webinterface you now have to add your new collection to the server
		a. Open interface in your browser (<IP>:8983/solr)
		b. Click on "Core Admin"
		c. Click on "Add Core"
			i. Name: The new name of your Collection, always use a machine readable name! (e.g. test_core)
			ii. instanceDir: The full path to your core (e.g. /etc/solr/solr-4.9.0/mysolr/solr/test_core)
			iii. dataDir: The full path to your core data directory (e.g. /etc/solr/solr-4.9.0/mysolr/solr/test_core/data)
			iv. Config: the full path to your core solrconfig.xml (e.g. /etc/solr/solr-4.9.0/mysolr/solr/test_core/conf/)
			v. Config: the full path to your core schema.xml (e.g. /etc/solr/solr-4.9.0/mysolr/solr/test_core/conf/)
		d. Click on "Add core"

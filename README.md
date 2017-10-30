# payara-hazelcast-aws
Demo of Hazelcast-AWS plugin using DiscoveryStrategy configuration

### Run The Demo
This ***MUST*** be run on EC2 instances only; the discovery strategy will ***NOT*** work outside of AWS infrastructure. (When doing this 'for real', additional discovery strategies can be combined). The `rest-jcache` example from Payara-Examples has been built into an Uber JAR with Payara Micro 173.

1. Replace the asterisks with valid access/secret keys for the AWS account you want to use.
2. Start the Payara Micro Uber JAR on each instance as follows, using `--addjars` to add the Hazelcast-AWS plugin and `--hzconfigfile` to add the `hazelcast.xml` file:

```
java -jar payara-micro-rest-jcache.jar --addjars hazelcast-aws-2.1.0.jar --hzconfigfile hazelcast.xml
```

3. Use an HTTP GET with curl Server1 to get the default response:

```
➜  ~ curl http://server1:8080/rest-jcache-1.0-SNAPSHOT/webresources/cache\?key\=test
helloworld%
```

4. Use an HTTP PUT on Server2 to add a value for key `test`
```
➜  ~ curl -H "Accept: application/json" -H "Content-Type: application/json" -X PUT -d "{data}" http://server2:8080/rest-jcache-1.0-SNAPSHOT/webresources/cache\?key\=test
```

5. Use another HTTP GET on Server1 to show the added data is available on both nodes

```
➜  ~ curl http://server1:8080/rest-jcache-1.0-SNAPSHOT/webresources/cache\?key\=test
{data}%
```

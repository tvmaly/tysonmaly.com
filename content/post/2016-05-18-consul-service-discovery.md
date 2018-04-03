---
author: admintm
categories:
- devops
- Go
date: "2016-05-18T20:10:28Z"
guid: http://www.tysonmaly.com/?p=187
id: 187
title: Consul Service Discovery and leader election
url: /devops/consul-service-discovery/
---

## Elect a leader with Consul for your service

So I started testing out a service discovery platform called Consul by the company Hashicorp.

The system uses the raft consensus protocol, and you may run into issues with leader election when you try to restart each server node.  I did, and before you start spending hours <a href="https://github.com/hashicorp/consul/issues/993" target="_blank" rel="nofollow">googling around</a>, I am going to tell you what I did to elect a leader in my cluster.

Here is how you can get your nodes to elect a leader.

First, make sure that your peers.json file has a set of ip addresses in it that refer to your server nodes.

The peers.json file is located in the -data-dir directory that you specified when you started up the agents running as servers.  Here is an example of how the file should look for 3 server nodes, each ip address is for the agents that are run as servers, not clients:

<pre>[
 "123.456.789.1",
 "123.456.789.2",
 "123.456.789.3"
]
</pre>

&nbsp;

Next, you can create a session with an associated key.  See the Hashicorp documents on <a href="https://www.consul.io/docs/guides/leader-election.html" target="_blank" rel="nofollow">leader elections</a> they state   &#8220;If the key has no associated `Session`, then there is no leader&#8221;

So you will want to create a session ID and for your <key> acquire that session ID.  The protocol used by consul will attempt to assign a leader when you perform this process.

To check if you were successful in electing a leader you can run the following command against the HTTP API that consul provides using curl on one of your nodes running the agent.

<pre>curl http://localhost:8500/v1/status/leader</pre>

If you were successful, you will get back a result that references one of your agent nodes being run as server.

You may come across an issue filed under the github project mentioning consul.json  config file.  This did not work at all for me, so save your time.

If you run the command:

<pre>consul info</pre>

You may still see some reference about leadership being false, but for your service, if you query the HTTP API then you will see a leader for it.   Please note, the HTTP API will not do round robin load balancing, if you want consul to perform round robin load balancing of your service, you will have to use the DNS api.

Assuming your service is named web, you would run this command on one of your nodes:

<pre>dig @127.0.0.1 -p 8600 web.service.consul</pre>

If you run it multiple times, you will see a different server node being returned in the first position each time.

&nbsp;
# 1. Create a new flume configuration file with the following.

``` netcat.conf
# Name the components on this agent
agent1.sources = netcat-source
agent1.sinks = logger-sink
agent1.channels = memory-channel

# Describe/configure the source
agent1.sources.netcat-source.type = netcat
agent1.sources.netcat-source.bind = localhost
agent1.sources.netcat-source.port = 44444
agent1.sources.netcat-source.channels = memory-channel

# Describe the sink
agent1.sinks.logger-sink.type = logger
agent1.sinks.logger-sink.channel = memory-channel

# Use a channel which buffers events in memory
agent1.channels.memory-channel.type = memory
agent1.channels.memory-channel.capacity = 1000
agent1.channels.memory-channel.transactionCapacity = 100
```

# 2. Start the agent.

```
$ flume-ng agent --conf /etc/flume-ng/conf --conf-file $DEVSH/exercises/flume/netcat.conf --name agent1 -Dflume.root.logger=INFO,console
```

# 3. From another terminal start telnet and connect to port 4444. Start typing and you should see the results from the other terminal. Provide a screenshot of your results.

```
$ telnet localhost 44444
```
<img width="747" alt="telnet" src="https://user-images.githubusercontent.com/16662143/55769166-b8a8d500-5aba-11e9-8d74-55616f448e5c.png">

<img width="966" alt="result" src="https://user-images.githubusercontent.com/16662143/55769154-b0509a00-5aba-11e9-9cdb-aeeee8a94bf7.png">

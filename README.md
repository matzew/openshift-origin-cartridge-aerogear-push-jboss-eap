# OpenShift AeroGear Push Server Cartridge

Provides the _AeroGear UnifiedPush Server_ running on top of JBoss Application Server on OpenShift. 

The [AeroGear UnifiedPush Server](https://github.com/aerogear/aerogear-unifiedpush-server) is a server that allows sending push notifications to different (mobile) platforms. The initial version of the server supports [Apple’s APNs](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9) and [Google Cloud Messaging](http://developer.android.com/google/gcm/index.html).

### Installation
The AeroGear Push Server cartridge defaults to using MySQL. When creating your application, you'll also want to add the MySQL cartridge:

```
rhc app create --no-git <APP> https://cartreflect-claytondev.rhcloud.com/reflect?github=aerogear/openshift-origin-cartridge-aerogear-push-jboss-eap
```

### Getting started with the AeroGear UnifiedPush Server

#### Administration Console

Once the server is running access it via ```http://{APP}-{NAMESPACE}.rhcloud.com```. Check the Administration console [user guide](http://aerogear.org/docs/guides/AdminConsoleGuide/) for more information on using the console.

**NOTE:** Besides the __Administration console_, the server can be accessed over RESTful APIs, as explained in the _AeroGear UnifiedPush Server_ [README](https://github.com/aerogear/aerogear-unified-push-server/blob/master/README.md). When executing the curl commands specified, you'll need to replace all instances of ```http://localhost:8080/ag-push``` with your OpenShift application URL ```http://{APP}-{NAMESPACE}.rhcloud.com```. 

#### Login

Temporarily, there is an "admin:123" user.  On _first_ login,  you will need to change the password.

	### Template Repository Layout

      .openshift/        Location for OpenShift specific files
      action_hooks/    See the Action Hooks documentation [1]
      markers/         See the Markers section [2]

\[1\] [Action Hooks documentation](https://github.com/openshift/origin-server/blob/master/node/README.writing_applications.md#action-hooks)
\[2\] [Markers](#markers)


### Environment Variables

The `aerogear-push` cartridge provides several environment variables to reference for ease
of use:

    OPENSHIFT_AEROGEAR_PUSH_EAP_IP                         The IP address used to bind JBossAS
    OPENSHIFT_AEROGEAR_PUSH_EAP_HTTP_PORT                  The JBossAS listening port
    OPENSHIFT_AEROGEAR_PUSH_EAP_CLUSTER_PORT               
    OPENSHIFT_AEROGEAR_PUSH_EAP_MESSAGING_PORT             
    OPENSHIFT_AEROGEAR_PUSH_EAP_MESSAGING_THROUGHPUT_PORT  
    OPENSHIFT_AEROGEAR_PUSH_EAP_REMOTING_PORT              
    JAVA_OPTS_EXT                                      Appended to JAVA_OPTS prior to invoking the Java VM

For more information about environment variables, consult the
[OpenShift Application Author Guide](https://github.com/openshift/origin-server/blob/master/node/README.writing_applications.md).

### Markers

Adding marker files to `.openshift/markers` will have the following effects:

    enable_jpda          Will enable the JPDA socket based transport on the java virtual
                         machine running the JBoss AS 7 application server. This enables
                         you to remotely debug code running inside the JBoss AS 7
                         application server.

    java7                Will run JBossAS with Java7 if present. If no marker is present
                         then the baseline Java version will be used (currently Java6)


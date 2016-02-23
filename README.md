# Camel Geocoder Component Example

This is a simple example of a Camel route based on the Camel-quartz2 component.
This route will be deployed on Apache Servicemix or Karaf.

# Setting up Karaf

This example is based on Camel 2.16.2 version.

- Download the Apache Karaf 3.0.5 package from: http://karaf.apache.org/index/community/download/karaf-3.0.5-release.html

- Unzip the package in a directory (we denote this folder with $KARAF_HOME)

- Execute $KARAF_HOME/bin/karaf

- Inside Karaf execute the following instructions:

```shell

karaf@root> feature:repo-add camel 2.16.2

```

- Now we need to install the features required by this bundle

```shell

karaf@root> feature:install camel-core
karaf@root> feature:install camel-spring
karaf@root> feature:install camel-quartz2

```

- We've almost done. We need to compile our project. In another terminal (and inside the project directory) executes the following command:

```shell

mvn clean package

```

- Now go back to Karaf and run

```shell

karaf@root> bundle:install -s file:///<project-directory>/target/camel-quartz2-example-1.0.0-SNAPSHOT.jar

karaf@root> log:tail

```

- In the log you should see

```shell

2016-02-23 13:49:21,690 | INFO  | ExtenderThread-2 | OsgiSpringCamelContext           | 70 - org.apache.camel.camel-core - 2.16.2 | Apache Camel 2.16.2 (CamelContext: camel1) is starting
2016-02-23 13:49:21,691 | INFO  | ExtenderThread-2 | ManagedManagementStrategy        | 70 - org.apache.camel.camel-core - 2.16.2 | JMX is enabled
2016-02-23 13:49:21,778 | INFO  | ExtenderThread-2 | DefaultRuntimeEndpointRegistry   | 70 - org.apache.camel.camel-core - 2.16.2 | Runtime endpoint registry is in extended mode gathering usage statistics of all incoming and outgoing endpoints (cache limit: 1000)
2016-02-23 13:49:21,800 | INFO  | ExtenderThread-2 | QuartzComponent                  | 92 - org.apache.camel.camel-quartz2 - 2.16.2 | Create and initializing scheduler.
2016-02-23 13:49:21,802 | INFO  | ExtenderThread-2 | QuartzComponent                  | 92 - org.apache.camel.camel-quartz2 - 2.16.2 | Setting org.quartz.scheduler.jmx.export=true to ensure QuartzScheduler(s) will be enlisted in JMX.
2016-02-23 13:49:21,817 | INFO  | ExtenderThread-2 | StdSchedulerFactory              | 91 - org.quartz-scheduler.quartz - 2.2.1 | Using default implementation for ThreadExecutor
2016-02-23 13:49:21,819 | INFO  | ExtenderThread-2 | SimpleThreadPool                 | 91 - org.quartz-scheduler.quartz - 2.2.1 | Job execution threads will use class loader of thread: SpringOsgiExtenderThread-2
2016-02-23 13:49:21,825 | INFO  | ExtenderThread-2 | SchedulerSignalerImpl            | 91 - org.quartz-scheduler.quartz - 2.2.1 | Initialized Scheduler Signaller of type: class org.quartz.core.SchedulerSignalerImpl
2016-02-23 13:49:21,826 | INFO  | ExtenderThread-2 | QuartzScheduler                  | 91 - org.quartz-scheduler.quartz - 2.2.1 | Quartz Scheduler v.2.2.1 created.
2016-02-23 13:49:21,826 | INFO  | ExtenderThread-2 | RAMJobStore                      | 91 - org.quartz-scheduler.quartz - 2.2.1 | RAMJobStore initialized.
2016-02-23 13:49:21,830 | INFO  | ExtenderThread-2 | QuartzScheduler                  | 91 - org.quartz-scheduler.quartz - 2.2.1 | Scheduler meta-data: Quartz Scheduler (v2.2.1) 'DefaultQuartzScheduler-com.github.oscerd.camel-quartz2-example' with instanceId 'NON_CLUSTERED'
  Scheduler class: 'org.quartz.core.QuartzScheduler' - running locally.
  NOT STARTED.
  Currently in standby mode.
  Number of jobs executed: 0
  Using thread pool 'org.quartz.simpl.SimpleThreadPool' - with 10 threads.
  Using job-store 'org.quartz.simpl.RAMJobStore' - which does not support persistence. and is not clustered.

2016-02-23 13:49:21,830 | INFO  | ExtenderThread-2 | StdSchedulerFactory              | 91 - org.quartz-scheduler.quartz - 2.2.1 | Quartz scheduler 'DefaultQuartzScheduler-com.github.oscerd.camel-quartz2-example' initialized from an externally provided properties instance.
2016-02-23 13:49:21,830 | INFO  | ExtenderThread-2 | StdSchedulerFactory              | 91 - org.quartz-scheduler.quartz - 2.2.1 | Quartz scheduler version: 2.2.1
2016-02-23 13:49:21,842 | INFO  | ExtenderThread-2 | QuartzEndpoint                   | 92 - org.apache.camel.camel-quartz2 - 2.16.2 | Job myGroup.durableJobRoute (triggerType=CronTriggerImpl, jobClass=CamelJob) is scheduled. Next fire date is Tue Feb 23 13:49:22 CET 2016
2016-02-23 13:49:21,883 | INFO  | ExtenderThread-2 | OsgiSpringCamelContext           | 70 - org.apache.camel.camel-core - 2.16.2 | AllowUseOriginalMessage is enabled. If access to the original message is not needed, then its recommended to turn this option off as it may improve performance.
2016-02-23 13:49:21,883 | INFO  | ExtenderThread-2 | OsgiSpringCamelContext           | 70 - org.apache.camel.camel-core - 2.16.2 | StreamCaching is not in use. If using streams then its recommended to enable stream caching. See more details at http://camel.apache.org/stream-caching.html
2016-02-23 13:49:21,909 | INFO  | ExtenderThread-2 | OsgiSpringCamelContext           | 70 - org.apache.camel.camel-core - 2.16.2 | Skipping starting of route durableJobRoute as its configured with autoStartup=false
2016-02-23 13:49:21,909 | INFO  | ExtenderThread-2 | QuartzComponent                  | 92 - org.apache.camel.camel-quartz2 - 2.16.2 | Starting scheduler.
2016-02-23 13:49:21,909 | INFO  | ExtenderThread-2 | QuartzScheduler                  | 91 - org.quartz-scheduler.quartz - 2.2.1 | Scheduler DefaultQuartzScheduler-com.github.oscerd.camel-quartz2-example_$_NON_CLUSTERED started.
2016-02-23 13:49:21,910 | INFO  | ExtenderThread-2 | OsgiSpringCamelContext           | 70 - org.apache.camel.camel-core - 2.16.2 | Total 1 routes, of which 0 is started.
2016-02-23 13:49:21,910 | INFO  | ExtenderThread-2 | OsgiSpringCamelContext           | 70 - org.apache.camel.camel-core - 2.16.2 | Apache Camel 2.16.2 (CamelContext: camel1) started in 0.220 seconds
2016-02-23 13:49:21,917 | INFO  | ExtenderThread-2 | OsgiBundleXmlApplicationContext  | 79 - org.apache.servicemix.bundles.spring-context - 3.2.14.RELEASE_1 | Publishing application context as OSGi service with properties {org.springframework.context.service.name=com.github.oscerd.camel-quartz2-example, Bundle-SymbolicName=com.github.oscerd.camel-quartz2-example, Bundle-Version=1.0.0.SNAPSHOT}
2016-02-23 13:49:21,929 | INFO  | ExtenderThread-2 | ContextLoaderListener            | 84 - org.springframework.osgi.extender - 1.2.1 | Application context successfully refreshed (OsgiBundleXmlApplicationContext(bundle=com.github.oscerd.camel-quartz2-example, config=osgibundle:/META-INF/spring/*.xml))


```

- because our route doesn't have the autostartup set to true

- Now we start the route

```shell

karaf@root> camel:route-list

 Context        Route             Status              Total #       Failed #     Inflight #   Uptime        
 -------        -----             ------              -------       --------     ----------   ------        
 camel1         durableJobRoute   Stopped                   0              0              0                 

karaf@root()> camel:route-start durableJobRoute

karaf@root> camel:route-list

 Context        Route             Status              Total #       Failed #     Inflight #   Uptime         
 -------        -----             ------              -------       --------     ----------   ------         
 camel1         durableJobRoute   Started                   1              0              0   1.649 seconds  

```

- Now in the log you should see

```shell
2016-02-23 13:51:16,001 | INFO  | l for user karaf | OsgiSpringCamelContext           | 70 - org.apache.camel.camel-core - 2.16.2 | Route: durableJobRoute started and consuming from: Endpoint[quartz2://myGroup/durableJobRoute?cron=0%2F2+*+*+*+*+%3F&durableJob=true&recoverableJob=true&trigger.repeatCount=3]
2016-02-23 13:51:16,009 | INFO  | example_Worker-8 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:16 CET 2016
2016-02-23 13:51:18,002 | INFO  | example_Worker-9 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:18 CET 2016
2016-02-23 13:51:20,001 | INFO  | xample_Worker-10 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:20 CET 2016
2016-02-23 13:51:22,002 | INFO  | example_Worker-1 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:22 CET 2016
2016-02-23 13:51:24,002 | INFO  | example_Worker-2 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:24 CET 2016
2016-02-23 13:51:26,001 | INFO  | example_Worker-3 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:26 CET 2016
2016-02-23 13:51:28,001 | INFO  | example_Worker-4 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:28 CET 2016
2016-02-23 13:51:30,002 | INFO  | example_Worker-5 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:30 CET 2016
2016-02-23 13:51:32,002 | INFO  | example_Worker-6 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:32 CET 2016
2016-02-23 13:51:34,001 | INFO  | example_Worker-7 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:34 CET 2016
2016-02-23 13:51:36,001 | INFO  | example_Worker-8 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:36 CET 2016
2016-02-23 13:51:38,002 | INFO  | example_Worker-9 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:38 CET 2016
2016-02-23 13:51:40,002 | INFO  | xample_Worker-10 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:40 CET 2016
2016-02-23 13:51:42,002 | INFO  | example_Worker-1 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:42 CET 2016
2016-02-23 13:51:44,001 | INFO  | example_Worker-2 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:44 CET 2016
2016-02-23 13:51:46,001 | INFO  | example_Worker-3 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:46 CET 2016
2016-02-23 13:51:48,002 | INFO  | example_Worker-4 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:48 CET 2016
2016-02-23 13:51:50,001 | INFO  | example_Worker-5 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:50 CET 2016
2016-02-23 13:51:52,001 | INFO  | example_Worker-6 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:52 CET 2016
2016-02-23 13:51:54,002 | INFO  | example_Worker-7 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:54 CET 2016
2016-02-23 13:51:56,002 | INFO  | example_Worker-8 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:56 CET 2016
2016-02-23 13:51:58,001 | INFO  | example_Worker-9 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:51:58 CET 2016
2016-02-23 13:52:00,002 | INFO  | xample_Worker-10 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:52:00 CET 2016
2016-02-23 13:52:02,002 | INFO  | example_Worker-1 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:52:02 CET 2016
2016-02-23 13:52:04,001 | INFO  | example_Worker-2 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:52:04 CET 2016
2016-02-23 13:52:06,001 | INFO  | example_Worker-3 | durableJobRoute                  | 70 - org.apache.camel.camel-core - 2.16.2 | Fired: Tue Feb 23 13:52:06 CET 2016

```

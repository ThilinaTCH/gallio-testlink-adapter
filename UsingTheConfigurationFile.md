# Introduction #

The TestlinkFixture is an attribute that is used to adorn Test suites in Nunit or MBUnit. It provides the basic info to allow the results of these tests to be exported to Testlink.
In the past, if any of these parameters had to be changed, the test suite had to be recompiled. Now it is possible to simply point to a configuration file and to provide all data in that configuration file


# Details #
## Changes to the TestLinkFixture Attribute ##
In the past the TestLinkFixture Attribute looked  like this:

```
    [TestLinkFixture(
        Url = "http://localhost/testlink/lib/api/xmlrpc.php",
        ProjectName = "TestLinkApi",
        UserId = "admin",
        TestPlan = "Automatic Testing",
        TestSuite = "nunitAddOn Sample Tests",
        PlatformName = "OS/2",
        DevKey = "fb37eb345a5b4f05659d5c35bb3465fd")]
```

## Using the ConfigFile option ##
Most of these data are most likely shared across all test suites - apart from the TestSuite name (which is the folder into which the test cases are stuck into).

So the new version will look like this:
```
    [TestLinkFixture(
    ConfigFile = "tlinkconfig.xml",
    TestSuite = "nunitAddOn Sample Tests")]
```

and the config file, called 'tlinkconfig.xml' will look like this

```
<?xml version="1.0" encoding="utf-8" ?>
<TestLinkFixtureConfiguration>
  <url value="http://localhost/testlink/lib/api/xmlrpc.php" override="yes" />
  <ProjectName  value="TestLinkApi" />
  <UserId value="admin"  override="yes" />
  <TestPlan value="Automatic Testing" />
  <PlatformName value="OS/2" />
  <DevKey value="fb37eb345a5b4f05659d5c35bb3465fd" override="yes" />
</TestLinkFixtureConfiguration>
```


So all parameters in the attribute (except  the ConfigFile one itself) can be located in the configfile.
Note the optional attribute called 'override="yes"'.
this is an important setting. The values in the actual attribute take precedence over the values in the config file. This allows the user to set default values in the config file and override them in the test suite code. But if you want the config file to take precedence you need to specify: override="yes"
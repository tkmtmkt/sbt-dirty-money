sbt-dirty-money is a sbt plugin for cleaning Ivy2 cache. If you use `publish-local` to test plugins and libraries, and you find yourself clearing Ivy2 cache often, this is a tool for you.

## latest
0.0.1

## how to setup
Add the following to your `~/.sbt/plugins/build.sbt`:

    addSbtPlugin("com.eed3si9n" % "sbt-dirty-money" % "X.X.X")

## how to use
The above automatically adds two global tasks to sbt prompt `clean-cache` and `clean-local` along with some settings like `clean-cache-files` and `clean-local-files`.

To display what `clean-cache` would clean, run:

    > show clean-cache-files
    [info] ArrayBuffer(/Users/foo/.ivy2/cache/scala_2.9.1/sbt_0.11.0/org.scalaxb/sbt-scalaxb, /Users/foo/.ivy2/cache/scala_2.9.1/sbt_0.11.0/org.scalaxb/sbt-scalaxb/jars/sbt-scalaxb-0.6.6-SNAPSHOT.jar)

**NOTE**: This is calculated as `((dir / "cache") ** ("*" + organization + "*") ** ("*" + name + "*")).get` where dir is `~/.Ivy2`. **If there are related projects that include both your `organization` and `name`, they would also be cleaned from the cache!** (For example, `unfiltered/unfiltered` would pick up any `unfiltered-xxx`). To delete the files, run:

    > clean-cache

Similarly, display what `clean-local` would clean, run:

    > show clean-local-files
    [info] ArrayBuffer(/Users/foo/.ivy2/local/org.scalaxb ...

This is calculated as `((dir / "local") ** ("*" + organization + "*") ** ("*" + name + "*")).get`. To delete these files, run:

    > clean-local
    
You probably want to clean cache if you clean local.

## License
MIT License. It's already in the license, but THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
Seriously, check what you're about to delete, and use it at your own risk.
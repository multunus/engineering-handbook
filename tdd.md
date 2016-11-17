# TDD, Some Untold Secrets
Other than the usual procedure and perks of following TDD, there are a few things that you come to realize about TDD once you really get down to practising it for a while. Some of these aspects might be rather subtle while others are theoretically obvious but practically a little harder to observe when starting out with TDD. Let's go through some of them. The ideas mentioned below are most applicable for unit/functional tests.

<a href="http://www.multunus.com/wp-content/uploads/2016/11/tdd-quote-bill-hetzel.png"><img class="aligncenter size-full wp-image-6177" src="http://www.multunus.com/wp-content/uploads/2016/11/tdd-quote-bill-hetzel.png" alt="tdd-quote-bill-hetzel" width="305" height="360" /></a>

## Executing TDD The Right Way
Uncle Bob defined the [three laws of TDD](http://butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd):
<ol>
 	<li>You are not allowed to write any production code unless it is to make a failing unit test pass.</li>
 	<li>You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.</li>
 	<li>You are not allowed to write any more production code than is sufficient to pass the one failing unit test.</li>
</ol>
Pretty easy, right? You later come to realize that these are more than just simple instructions. They are a set of guidelines that help you not only follow the practice of TDD, but also reap the benefits of it:
<ul>
 	<li><strong>All</strong> the code you write will be testable, further implying that it will be quite decoupled since that is a requirement to test a module in isolation.</li>
 	<li>You can clean up messy code without any fear that you'll unknowingly break something. The tests can catch any such changes immediately.</li>
 	<li>Tests serve as documentation in themselves! Every line of code you write is backed up by one or more tests, which if well phrased can explain exactly what the code does without any extra effort.</li>
</ul>
There are additional benefits that are explained below.

## Immediate Feedback
When following TDD, the tendency is to run the tests more frequently. Maybe not the entire test suite all the time, but at least the tests pertaining a particular method or class will get run very often. This is a natural outcome of TDD. The resulting advantage is that you get instantaneous feedback on several areas:
<ul>
 	<li>If the test you wrote passes without any additional code, then you know that the test is *probably* flawed and needs to be improved.</li>
 	<li>Each test is run as it is created, and hence ensures that there is a check for each scenario that is going to be introduced into the code. Once the code is written, the test also verifies that it is working as expected.</li>
 	<li>The code grows more organically and every point after a test passes is a potential point for refactoring. The only thing to check after refactoring is whether the tests still pass! This already results in better quality code.</li>
 	<li>Regression testing happens on the fly! This is one of the more subtle advantages that you do not see until you are dealing with a big-enough codebase. As you add more code and run the tests on the fly, you're checking not only the functionality of new code, but also that whatever functionality was previously there is still preserved (unless of course the new code intentionally modifies it!).</li>
</ul>

## Impact on Productivity
This is probably going to be counter-intuitive, but following TDD is actually going to increase productivity! This is something that has been both experienced by our folks and [scientifically proven](http://nparc.cisti-icist.nrc-cnrc.gc.ca/eng/view/accepted/?id=0420df64-f474-4072-8df6-c7b87c0de643).

In a nutshell, here's what happens. TDD forces you to write functionality, one logical increment (does that even make sense?!) at a time. So you are indirectly spiraled into a continuous cycle of creating small tests and writing just enough code to make them pass. Since these activities are sufficiently small, they can be accomplished fast and result in both higher satisfaction and better focus. In geek terminology, this is a recursive loop!

#### The Ping Pong Pattern
In addition to following TDD, if you're practising pair programming, there's an interesting pattern that the pair can follow. It's called the [Ping Pong pattern](http://c2.com/cgi/wiki?PairProgrammingPingPongPattern). The idea is simple - the pair comprises two programmers, Frank and Lois. programmer Frank writes a new failing test. Lois implements the code to get the test passing then writes the next failing test. Now Frank writes code to pass the test. And the cycle repeats. This greatly improves focus, flow and hence productivity.

## Help! Slow Tests!
If your test suite is running really slowly, that's probably feedback that something is not right. There are a couple of common reasons why your tests run slowly, and these are described below.

#### Network requests
In order to have really independent tests, your tests should not make any network requests. Instead, these requests should be stubbed or mocked to mimic the behaviour of the service to which the requests are sent. There are usually a couple of ways to accomplish this:
<ul>
 	<li>Simply stub the network request method calls to return the apt value</li>
 	<li>Use a mocking library that automatically returns the response when the request is raised</li>
 	<li>Fire up a mock server that behaves just like the service the test contacts</li>
</ul>
Of course the option that you choose ultimately depends on how important it is to test the network request itself. If you're dealing with a less critical task such as fetching a simple number, you could go with a simple stub. However, for more complicated ones such as testing more complicated requests to other microservices, you'd probably want to have a more accurate response mechanism and could go for one of the last 2 options.

#### Too much test setup
This is probably a smell rather than the problem itself. The most likely culprit if you find yourself writing so much setup is the lack of sufficient modularisation. The methods are handling too much responsibility than is necessary. If the implementation comprises several computationally intensive procedures, then your test is bound to run slowly. Rely on TDD itself to come up with better methods. Plan out how to write better and smaller methods that you can easily stub if required. This also results in more maintainable code.

#### Over-reliance on persistence of records
As fast as database queries are, relying too much on having all the necessary records persisted will slow down your tests. At a granular level, the difference may not be significant. However, considering the test suite as a whole, half a second more for each test can make a huge difference! Try and use more stubbed objects. These are bound to be quite fast and will reduce the test suite run time considerably.

#### A Quick Fix for Slow Tests
Since tests are usually (and ideally) not dependent on each other, they can be run in parallel without messing up anything. Of course this can only be stretched as far as the available resources in the system. For a single-core machine, parallel tests may not yield significant gains. Pushing the machine too hard can even increase run time since there's the overhead of maintaining the parallel system. The ideal case is to probably have as many parallel lines as there are cores in the system.

There's also an added disadvantage, though very minor, that you'll need multiple databases for each parallel line of tests.

## So what can I do now?
It's never easy to start on TDD since it requires a different kind of thinking to write 'code' that will test the actual code you'll be writing. But with practice, it can easily become second nature. I'd recommend starting with a well-supported platform such as Ruby + RSpec to ensure setting the sails goes as smoothly as possible, although this may vary depending on experience you may already have with other languages and testing frameworks.

Also, please feel free to reach out if you have any questions or thoughts.
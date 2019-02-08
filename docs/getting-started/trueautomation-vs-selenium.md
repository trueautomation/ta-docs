# [TrueAutomation.io](https://trueautomation.io/) vs Selenium

One of the main tasks of TrueAutomation.io is to solve problem of working with unstable locators. The Object Repository and Smart Locators are exactly used for this. But as a matter of fact - they are not actually locators.
A regular locator that is currently used in many tools is actually a path to the element that is dependent on technology, page hierarchy, etc. That is why, whenever anything is changed, the locator is not valid anymore. That’s the reason why we have moved away from the idea of using old-school locators. The whole idea of them is broken and requires tons of maintenance.

What we call a Smart Locator is a unique footprint of an element. This is how we build it:
During the first API call we collect information on elements, element attributes, dependencies between elements, page information. Once information is collected we build a unique footprint of the element based on it. That allows us not to depend on actual locators and thus minimize further maintenance and guarantee, that the element will be found even if it is dramatically changed. In other words, TrueAutomation Smart Locator is just and an alias for the set of unique parameters that characterize a particular element and helps us find it.

The Object Repository is a collection of object and properties. Initially, it is designed for caching of test objects. Afterwards, one you have already objects in the repository, it will help to detect elements on the web page more precisely even in case when their parameters were partially changed. Objects are added to your project repository when you run tests with them in TrueAutomation for the 1st time. Thus, TA will solve this problem when Selenium doesn’t perform such functions at all.

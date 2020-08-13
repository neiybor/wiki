<!-- TITLE: Amplitude Migration -->
<!-- SUBTITLE: A quick summary of Amplitude Migration -->

# Meetings
[2020-08-11](https://wiki.neighbor.com/engineering/growth/amplitude-migration/2020-08-11)
[2020-08-18](https://wiki.neighbor.com/engineering/growth/amplitude-migration/2020-08-18)

# Documents
[Activation Plan](https://docs.google.com/spreadsheets/d/1VelXZKa1y9ZIM8we2viJ2xv9hrZ1B3xg77gVbvIgcvs/edit?usp=sharing)
[Event & Property Migration](https://docs.google.com/spreadsheets/d/1A7IVwDa55c_22e7ZnrI-jNxbRwuR4NWHFM4TV4c7uK8/edit?usp=sharing)

# Resources
[A/B Testing Best Practices](https://help.amplitude.com/hc/en-us/articles/115001580108-How-to-Analyze-A-B-Tests-Results-in-Amplitude)
[Data Taxonomy](https://help.amplitude.com/hc/en-us/articles/115000465251-Data-Taxonomy-Playbook)

# Internal Q & A
## Do we need a full history of user properties?
 * 12M out of the 20M events from an extract of the last 7 months are user property updates
 * If we only keep the last user property update, it reduces to about 400K
## How do we want to store AB test assignments?
* Use properties?
	* property per event - lots of properties, is this a big deal?
	* single property array - complicates atomicity of test assignment because we are mutating a property 
* Use events
	* LOTS of events - but we could probably reduce them quite a lot too
## Should we use Segment "cloud-mode" or "device-mode"
* [Segment overview](https://segment.com/docs/connections/destinations/#connection-modes)

## Do we want to use track calls (individual events) or page calls (Track Named Pages/Track Categorized Pages setting) when viewing a page?
* [Segment Overview](https://segment.com/docs/connections/destinations/catalog/amplitude/#client-and-server)

## Do we track events as actions that users have done or by the pages that they have loaded?

## Event & property nomenclature
Amplitude recommendation:
EVENTS
* All lower case
* Spaces between words
* Present tense verb + object

PROPERTIES
* All lowercase
* If not a string value, refer the property's value type e.g. **is** subscriber = true/false , **num** of purchases = [1. 2. 3]

Kavitha event name examples:
* Application Installed - noun + verb, capital with spacing
* Clicked clear filters - verb + noun, first word capital with spacing
* clearIdentity - verb unclear, camel case
* EmailVerified - noun + verb, capital without spacing
* logERROR - no verb, caps lock without spacing

(Colton) I recommend we use Amplitude's recommendation. Do not use client name in event name.

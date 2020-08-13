<!-- TITLE: Amplitude Migration -->
<!-- SUBTITLE: A quick summary of Amplitude Migration -->

# Meetings
[2020-08-11](https://wiki.neighbor.com/engineering/growth/amplitude-migration/2020-08-11)

# Documents
[Kavitha's Tracking Google Doc](https://docs.google.com/spreadsheets/d/1VelXZKa1y9ZIM8we2viJ2xv9hrZ1B3xg77gVbvIgcvs/edit?usp=sharing)
[A/B Testing Best Practices](https://help.amplitude.com/hc/en-us/articles/115001580108-How-to-Analyze-A-B-Tests-Results-in-Amplitude)

# Q & A
## Do we need a full history of user properties?
## How do we want to store AB test assignments?
* Use properties?
	* property per event - lots of properties, is this a big deal?
	* single property array - complicates atomicity of test assignment because we are mutating a property 
* Use events
	* LOTS of events - but we could probably reduce them quite a lot too

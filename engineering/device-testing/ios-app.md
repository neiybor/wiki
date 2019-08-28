<!-- TITLE: iOS App -->
<!-- SUBTITLE: iOS Device Testing -->

# Test Suite
***If you find a bug or something wrong:***
	1. Take a screenshot if you can
	2. Write down quick description of bug
	3. Send to Paul via email/slack

***If you need a test device, come to the mobile apps room.***
## Host Experience
1. Create a new listing as a new user
2. Create a new listing as a current user
3. Edit a listing
	a. Change Address
	b. Change Listing Title
	c. Change Price
	d. Change First Month Discount
	e. Change Photos
	f. Share an unreserved listing
	g. Archive & Unarchive an unreserved listing
4. Test Inbox
	a. Send a few messages (some very long ones too)
	b. View user profile from conversation
	c. Turn off wifi and make sure you can't send a message
	d. Verify that most recent messages/conversations are at the top of the inbox
5. Test Progress Page (click individual listings to access these) - verify correctness on progress page after each test
	a. Test earnings by viewing payout sheet for some listings and verifying correctness
	b. Test page views by promoting some listings
	c. Test price score by changing some listings' prices to be too high, too low, and just right (listings without cities/states will not have a recommended price range displayed)
	d. Test First Month Discount by turning it on and off for some listings
6. Test Profile Page
	a. Siri Shortcuts - add a phrase if one is not already there, use the shortcut
	b. Review Our App - test both thumbs up (verify it goes to app store) and thumbs down (send negative feedback), DO NOT leave a review on the app store
	c. Trust And Safety - Verify Trust and Safety Page shows
	d. Help - Verify both options (FAQ page shows, intercom shows)
## Renter Experience
1. Reserve Listing through new Search flow
2. Save some listings
	a. Save multiple listings
	b. Reserve a listing from your saved list
	c. Delete all saved listings
3. Send some referrals/invites as a new user
	a. Send an invite to one email
  b. Send an invite to several emails (at once)
	c. View Track Referrals and verify correctness
  d. View Leaderboard and verify correctness
4. Use the Referral Rank Demo/Tutorial (Referral > Track Referrals > How do I improve my rank?)
  a. Try each of the options
	b. Use "Snap back to reality"
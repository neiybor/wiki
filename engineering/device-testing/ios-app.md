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
	c. Test price score by changing some listings' prices to be too high, too low, and just right
	d. Test First Month Discount by turning it on and off for some listings
6. Test Profile Page
	a. Siri Shortcuts - add a phrase if one is not already there, use the shortcut
	b. Review Our App - test both thumbs up (verify it goes to app store) and thumbs down (send negative feedback), DO NOT leave a review on the app store
	c. Trust And Safety - Verify Trust and Safety Page shows
	d. Help - Verify both options (FAQ page shows, intercom shows)
## Renter Experience
1. Test Reserving Listings
  a. Reserve Listing through new normal flow (use filters and verify correctness/quality of results)
	b. Reserve listing via 3D touch if available
2. Save some listings
	a. Save multiple listings
	b. Save some listings via 3D touch if available
	b. Reserve a listing from your saved list
	c. Delete all saved listings
3. Test Rentals Page
	a. Verify correctness of pending reservations and rented space
	b. Test a Pending Reservation (click into a pending reservation)
		i. Click listing title and verify correct listing detail page is showing
		ii. Click Next Steps verify info is correct and address is not showing
		iii. Click Message and verify you are messaging the host, send some messages
		iv. Click Cancel and Confirm cancellation, verify listing is no longer in pending reservations
	c. Test A Rented Space (click into a rented space)
		i. Same as above
		ii. Click Next Steps, verify correct info and address is showing, click address to verify link to maps/directions
		iii. Same as above
		iv. Same as above (except verify the listing is no longer in rented space)
4. Send some referrals/invites as a new user
	a. Send an invite to one email
  b. Send an invite to several emails (at once)
	c. View Track Referrals and verify correctness
  d. View Leaderboard and verify correctness
5. Use the Referral Rank Demo/Tutorial (Referral > Track Referrals > How do I improve my rank?)
  a. Try each of the options
	b. Use "Snap back to reality", verify data is correct
6. Test Profile Page
	a. Public Information - Change public info, save changes, and verify that the changes were saved
	b. Private Information - Reverify Phone Number, Change Password
	c. Payment Methods - Test Pay as a Renter, enter in credit card ('42' repeated until it is completely filled), verify Manage Host Payments brings up Stripe Dashboard
	d. App Icons - change the app icon a few times and verify it actually changes
7. Test Host Onboarding (on an account that is not a host) Profile > Learn about hosting
		a. Click "See how much you could earn", verify listing calculator shows
		b. Change input on listing calculator and verify earnings change
		c. Click "Learn more about trust and safety" on second page, verify trust and safety page shows
		d. Verify Yearly Potential reflects earnings from earnings calculator
		e. Verify List Your Space button starts listing creation flow
		f. Go back to renter profile page and verify potential earnings is still correct